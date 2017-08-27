ANDROID_TOP_DIR=$(shell realpath ../../../..)

CPPFLAGS+= \
    -fPIC \
    -I$(ANDROID_TOP_DIR)/frameworks/native/include \
    -I$(ANDROID_TOP_DIR)/system/core/include \
    -I$(ANDROID_TOP_DIR)/libnativehelper/include
LDFLAGS+= -shared

SOURCES = \
    AppOpsManager.cpp \
    Binder.cpp \
    BpBinder.cpp \
    BufferedTextOutput.cpp \
    Debug.cpp \
    IAppOpsCallback.cpp \
    IAppOpsService.cpp \
    IBatteryStats.cpp \
    IInterface.cpp \
    IMediaResourceMonitor.cpp \
    IMemory.cpp \
    IPCThreadState.cpp \
    IPermissionController.cpp \
    IProcessInfoService.cpp \
    IResultReceiver.cpp \
    IServiceManager.cpp \
    MemoryBase.cpp \
    MemoryDealer.cpp \
    MemoryHeapBase.cpp \
    Parcel.cpp \
    PermissionCache.cpp \
    PersistableBundle.cpp \
    ProcessInfoService.cpp \
    ProcessState.cpp \
    Static.cpp \
    Status.cpp \
    TextOutput.cpp \

OBJECTS=$(patsubst %.cpp,%.o,$(SOURCES))

TARGET=libbinder.so

all: $(TARGET)

$(TARGET): $(OBJECTS)
	$(CXX) $(CPPFLAGS) $(OBJECTS) -o $@ $(LDFLAGS)

%.o: %.cpp
	$(CXX) -c $(CPPFLAGS) -o $@ $<

clean:
	rm -rf $(OBJECTS) $(TARGET)

install:
	install -m 0644 $(TARGET) $(DESTDIR)/usr/lib/$(TARGET)

.PHONY: clean install all
