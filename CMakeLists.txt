cmake_minimum_required(VERSION 3.22.1)

project(Zelda3)

include(FindPkgConfig)
include(resources.cmake)

find_package(SDL2)

set(SNES_SOURCES snes/apu.c snes/apu.h snes/cart.c snes/cart.h snes/cpu.c snes/cpu.h snes/dma.c snes/dma.h snes/dsp.c snes/dsp.h snes/dsp_regs.h snes/input.c snes/input.h snes/ppu.c snes/ppu.h snes/saveload.h snes/snes.c snes/snes.h snes/snes_other.c snes/snes_regs.h snes/spc.c snes/spc.h snes/types.h snes/tracing.c snes/tracing.h)

add_library(snes ${SNES_SOURCES})

target_include_directories(snes PUBLIC snes)
target_include_directories(snes PRIVATE zelda)

set(ZELDA_SOURCES zelda/ancilla.c zelda/ancilla.h zelda/attract.c zelda/attract.h zelda/config.c zelda/config.h zelda/dungeon.c zelda/dungeon.h zelda/ending.c zelda/ending.h zelda/hud.c zelda/hud.h zelda/load_gfx.c zelda/load_gfx.h zelda/main.c zelda/messaging.c zelda/messaging.h zelda/misc.c zelda/misc.h zelda/nmi.c zelda/nmi.h zelda/overlord.c zelda/overlord.h zelda/overworld.c zelda/overworld.h zelda/player.c zelda/player.h zelda/player_oam.c zelda/player_oam.h zelda/poly.c zelda/poly.h zelda/select_file.c zelda/select_file.h zelda/spc_player.c zelda/spc_player.h zelda/sprite.c zelda/sprite.h zelda/sprite_main.c zelda/sprite_main.h zelda/tagalong.c zelda/tagalong.h zelda/tile_detect.c zelda/tile_detect.h zelda/variables.h zelda/zelda_cpu_infra.c zelda/zelda_cpu_infra.h zelda/zelda_rtl.c zelda/zelda_rtl.h ${RESOURCE_COMPILED_FILES})

add_executable(zelda3 ${ZELDA_SOURCES})

add_dependencies(zelda3 compile_resources)

target_include_directories(zelda3 PRIVATE snes tables ${SDL2_INCLUDE_DIRS})
target_link_libraries(zelda3 PRIVATE snes ${SDL2_LIBRARIES})

