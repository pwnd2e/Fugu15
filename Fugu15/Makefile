.PHONY: all clean build_clean

all: Fugu15.ipa

Fugu15.ipa: build/Build/Products/Debug-iphoneos/Fugu15.app
	@echo Ad-Hoc signing Fugu15
	codesign -s - --entitlements Fugu15/Fugu15.entitlements build/Build/Products/Debug-iphoneos/Fugu15.app
	@echo Fake-signing Fugu15
	../Tools/fastPathSign/fastPathSign build/Build/Products/Debug-iphoneos/Fugu15.app
	@echo Creating ipa
	rm -rf Payload Fugu15.ipa
	mkdir Payload
	cp -r build/Build/Products/Debug-iphoneos/Fugu15.app Payload/Fugu15.app
	unzip Payload/Fugu15.app/bootstrap.tar bootstrap.tar -d Payload/Fugu15.app/bootstrap
	rm -rf Payload/Fugu15.app/bootstrap.tar
	mv Payload/Fugu15.app/bootstrap/bootstrap.tar Payload/Fugu15.app/bootstrap.tar
	rm -rf Payload/Fugu15.app/bootstrap
	zip -Ar Fugu15.ipa Payload
	rm -rf Payload

build/Build/Products/Debug-iphoneos/Fugu15.app: FORCE
	xcodebuild -scheme Fugu15 -derivedDataPath build -destination 'generic/platform=iOS' CODE_SIGN_IDENTITY="" CODE_SIGNING_REQUIRED=NO

clean:
	rm -rf build Payload Fugu15.ipa

build_clean:
	rm -rf Payload build

FORCE: ;
