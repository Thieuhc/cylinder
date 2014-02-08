NAME=Cylinder
IPHONE_IP=iphone

CC=xcrun -sdk iphoneos clang
ARCH=-arch armv7 -arch arm64
SDKS=-mios-version-min=3.0 -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS7.0.sdk
#ARC=-fobjc-arc
FRAMEWORKS=-framework Foundation -framework UIKit -framework QuartzCore
FLAGS= -dynamiclib #-undefined suppress -flat_namespace
DYLIB=$(NAME).dylib
LIBLUA=lua/liblua.a

MS_DIR=/Library/MobileSubstrate/DynamicLibraries/
CYLINDER_DIR=/Library/Cylinder/

COMP=substrate/libsubstrate.dylib Tweak.m $(LIBLUA)
REQ=$(COMP) luashit.h luashit.m macros.h Makefile

all: $(DYLIB)

copy: $(DYLIB)
	scp $(DYLIB) $(IPHONE_IP):$(MS_DIR)
	scp $(NAME).plist $(IPHONE_IP):$(MS_DIR)
	scp -r scripts/* $(IPHONE_IP):$(CYLINDER_DIR)

clean:
	rm $(DYLIB)
	cd lua && $(MAKE) clean

$(DYLIB): $(REQ)
	$(CC) $(COMP) $(ARCH) $(SDKS) $(FRAMEWORKS) $(ARC) $(FLAGS) -o $@

$(LIBLUA): lua/Makefile
	cd lua && $(MAKE)