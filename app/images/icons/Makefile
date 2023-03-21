BROWSER_SIZES := 16 24 32 48 64
#ANDROID_SIZES := 72 96 144 192
# FIXME: The ICO is limited to 8 icons due to a Chrome bug:
#        https://bugs.chromium.org/p/chromium/issues/detail?id=1381393
ANDROID_SIZES := 96 144 192
WEB_ICON_SIZES := $(BROWSER_SIZES) $(ANDROID_SIZES)

#IOS_1X_SIZES := 20 29 40 76 # No such devices exist anymore
IOS_2X_SIZES := 40 58 80 120 152 167
IOS_3X_SIZES := 60 87 120 180
ALL_IOS_SIZES := $(IOS_1X_SIZES) $(IOS_2X_SIZES) $(IOS_3X_SIZES)

ALL_ICONS := \
	$(ALL_IOS_SIZES:%=sortium-ios-%.png) \
	sortium.ico

all: $(ALL_ICONS)

# Our testing shows that the ICO file need to be sorted in largest to
# smallest to get the apporpriate behviour
WEB_ICON_SIZES_REVERSE := $(shell echo $(WEB_ICON_SIZES) | tr ' ' '\n' | sort -nr | tr '\n' ' ')
WEB_BASE_ICONS := $(WEB_ICON_SIZES_REVERSE:%=sortium-%.png)
.INTERMEDIATE: $(WEB_BASE_ICONS)

# General conversion
sortium-%.png: sortium-favicon.svg
	cairosvg -W $* -H $* "$(lastword $^)" -o "$@"

# iOS icons use their own SVG
sortium-ios-%.png: sortium-favicon.svg
	cairosvg -W $* -H $* -b white "$(lastword $^)" -o "$@"

# The smallest sizes are generated using a different SVG
sortium-16.png sortium-24.png sortium-32.png: sortium-favicon.svg

clean:
	rm -f *.png
