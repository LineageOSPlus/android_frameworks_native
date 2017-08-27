ANDROID_TOP_DIR=$(shell realpath ../../../..)

CPPFLAGS+= \
    -fPIC \
    -pthread \
    -DBUILD_WITH_LINARO \
    -I$(ANDROID_TOP_DIR)/frameworks/native/include \
    -I$(ANDROID_TOP_DIR)/system/core/include \
    -I$(ANDROID_TOP_DIR)/system/core/base/include \
    -I$(ANDROID_TOP_DIR)/libnativehelper/include
LDFLAGS= \
    -pthread \
    -L$(ANDROID_TOP_DIR)/frameworks/native/libs/binder \
    -L$(ANDROID_TOP_DIR)/system/core/liblog \
    -L$(ANDROID_TOP_DIR)/system/core/libutils \
    -L$(ANDROID_TOP_DIR)/system/core/libcutils \
    -L$(ANDROID_TOP_DIR)/system/core/base \
    -lbinder \
    -llog \
    -lutils \
    -lcutils \
    -lbase

SOURCES = \
    dumpsys.cpp

OBJECTS=$(patsubst %.cpp,%.o,$(SOURCES))

TARGET=dumpsys

all: $(TARGET)

$(TARGET): $(OBJECTS)
	$(CXX) $(CPPFLAGS) $(OBJECTS) -o $@ $(LDFLAGS)

%.o: %.cpp
	$(CXX) -c $(CPPFLAGS) -o $@ $<

clean:
	rm -rf $(OBJECTS) $(TARGET)

install-deps: $(LIB_DEPS)
	$(foreach lib, $^, make -C $(dir $(lib)) install;)

install:
	install -m 0755 -D $(TARGET) $(DESTDIR)/usr/bin/$(TARGET)

install-all: install-deps install

.PHONY: clean install all

