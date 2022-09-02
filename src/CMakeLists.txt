cmake_minimum_required(VERSION 3.12)

set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")
set(CMAKE_BUILD_TYPE Debug)
include(pico_sdk_import.cmake)

project(sdiotest)
if (NOT TARGET sdiotest)
pico_sdk_init()

add_executable(sdiotest
    bench.cpp
    SdCardInfo.cpp
    #SdioTeensy.cpp
    sd_card.cpp
    #SdSpiCard.cpp
    extra/attic/PrintBasic.cpp
    #ExFatFile.
    ExFatLib/ExFatDbg.cpp
    ExFatLib/ExFatFile.cpp
    ExFatLib/ExFatFilePrint.cpp
    ExFatLib/ExFatFileWrite.cpp
    ExFatLib/ExFatFormatter.cpp
    ExFatLib/ExFatName.cpp
    ExFatLib/ExFatPartition.cpp
    ExFatLib/ExFatVolume.cpp
    FatLib/FatFile.cpp
    FatLib/FatDbg.cpp
    FatLib/FatFileLFN.cpp
    FatLib/FatFilePrint.cpp
    FatLib/FatFileSFN.cpp
    FatLib/FatFormatter.cpp
    FatLib/FatName.cpp
    FatLib/FatPartition.cpp
    FatLib/FatVolume.cpp
    FsLib/FsFile.cpp
    FsLib/FsNew.cpp
    FsLib/FsVolume.cpp
    common/FsCache.cpp
    common/FsDateTime.cpp
)

include_directories(sdiotest . extra/attic ../../../pico-sdk/src/rp2_common/hardware_gpio/include ../../../pico-sdk/src/rp2_common/hardware_dma/include ../../../pico-sdk/src/common/pico_time/include)



add_compile_definitions(sdiotest PRIVATE HAS_SDIO_CLASS USE_MULTI_SECTOR_IO)

target_link_libraries(sdiotest PRIVATE pico_stdlib hardware_pio)
endif()
pico_add_extra_outputs(sdiotest)

pico_generate_pio_header(sdiotest ${CMAKE_CURRENT_LIST_DIR}/sd_card.pio)
