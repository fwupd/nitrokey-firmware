VENDOR=Nitrokey
PROJECT_NAME=Storage
VERSION=0.47
DOWNLOAD_ROOT=https://github.com/Nitrokey/nitrokey-storage-firmware/releases/download/V0.47.0
FIRMWARE_FILE=firmware_V0.47.0.hex
METAINFO_FILE=storage.metainfo.xml

all: $(VENDOR)-$(PROJECT_NAME)-$(VERSION).cab

# cannot distribute in repo
$(FIRMWARE_FILE):
	wget $(DOWNLOAD_ROOT)/$@ -O $@

clean:
	rm -f *.cab *.dfu

check: $(METAINFO_FILE)
	appstream-util validate-relax $(METAINFO_FILE)

%.cab: $(FIRMWARE_FILE) $(METAINFO_FILE)
	gcab --create --nopath $@ $(FIRMWARE_FILE) $(METAINFO_FILE)
