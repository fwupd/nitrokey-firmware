VENDOR=Nitrokey
PROJECT_NAME=Storage
VERSION=0.53
DOWNLOAD_ROOT=https://github.com/Nitrokey/nitrokey-storage-firmware/releases/download/V${VERSION}
FIRMWARE_FILE=storage-firmware-V0.53-0-g905976e.hex
FIRMWARE_FILE_TARGET=firmware_V${VERSION}.0.hex 
SIGNATURE_FILE=$(FIRMWARE_FILE).sig
SHASUM_FILE=$(FIRMWARE_FILE).sha256sum
METAINFO_FILE=storage.metainfo.xml

all: $(VENDOR)-$(PROJECT_NAME)-$(VERSION).cab

# cannot distribute in repo
$(FIRMWARE_FILE) $(SHASUM_FILE) $(SIGNATURE_FILE):
	wget $(DOWNLOAD_ROOT)/$@ -O $@

clean:
	-rm -v *.cab *.dfu *.hex *.sig *.sha256sum

check_all:  check_sum check_sig check check_cab

check: $(METAINFO_FILE)
	appstream-util validate-relax $(METAINFO_FILE)

check_cab: $(VENDOR)-$(PROJECT_NAME)-$(VERSION).cab $(FIRMWARE_FILE)
	gcab -t $< 

check_sum: $(SHASUM_FILE) $(FIRMWARE_FILE) 
	sha256sum -c $<

check_sig: $(SIGNATURE_FILE) $(FIRMWARE_FILE)
	gpg2 --verify $<

%.cab: $(FIRMWARE_FILE) $(METAINFO_FILE)
	mv $(FIRMWARE_FILE) $(FIRMWARE_FILE_TARGET) -v
	gcab --create --nopath $@ $(FIRMWARE_FILE_TARGET) $(METAINFO_FILE)

.PHONY:
	clean check check_sig check_sum check_all check_cab
