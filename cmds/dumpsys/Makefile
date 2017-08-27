ANDROID_TOP_DIR=$(shell realpath ../../../..)

LIB_DEPS = \
    $(ANDROID_TOP_DIR)/frameworks/native/libs/binder/libbinder.so \
    $(ANDROID_TOP_DIR)/system/core/liblog/liblog.so \
    $(ANDROID_TOP_DIR)/system/core/libutils/libutils.so \
    $(ANDROID_TOP_DIR)/system/core/libcutils/libcutils.so \
    $(ANDROID_TOP_DIR)/system/core/base/libbase.so
LIB_DEPS_LDFLAGS = $(addprefix -L,$(dir $(LIB_DEPS))) \
                   $(addprefix -l,$(patsubst lib%.so, %, $(notdir $(LIB_DEPS))))

CPPFLAGS+= \
    -fPIC \
    -pthread \
    -I$(ANDROID_TOP_DIR)/frameworks/native/include \
    -I$(ANDROID_TOP_DIR)/system/core/include \
    -I$(ANDROID_TOP_DIR)/system/core/base/include \
    -I$(ANDROID_TOP_DIR)/libnativehelper/include
LDFLAGS= \
    -pthread \
    $(LIB_DEPS_LDFLAGS)

SOURCES = \
    dumpsys.cpp

OBJECTS=$(patsubst %.cpp,%.o,$(SOURCES))

TARGET=dumpsys

all: $(TARGET)

$(TARGET): $(OBJECTS) $(LIB_DEPS)
	$(CXX) $(CPPFLAGS) $(OBJECTS) -o $@ $(LDFLAGS)

%.so:
	make -C $(dir $@)

%.o: %.cpp
	$(CXX) -c $(CPPFLAGS) -o $@ $<

clean:
	rm -rf $(OBJECTS) $(TARGET)

clean-deps:
	$(foreach lib, $(LIB_DEPS), make -C $(dir $(lib)) clean;)

clean-all: clean clean-deps

install-deps: $(LIB_DEPS)
	$(foreach lib, $^, make -C $(dir $(lib)) install;)

install:
	install -m 0755 -D $(TARGET) $(DESTDIR)/usr/bin/$(TARGET)

install-all: install-deps install

.PHONY: clean install all

