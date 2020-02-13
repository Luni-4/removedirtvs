project('RemoveDirt', 'cpp',
        version: '1',
        default_options: ['cpp_std=c++11', 'buildtype=release'],
        meson_version: '>=0.46')


warnings = [
  '-Wall',
  '-Wextra',
  '-Wno-unused-parameter',
]

cflags = [
  warnings,
  '-fpermissive',
  '-DVS_TARGET_CPU_X86'
]

ldflags = [
]

host_cpu_family = host_machine.cpu_family()

if host_cpu_family.startswith('x86')
  cflags += ['-mfpmath=sse', '-msse2']
endif

host_system = host_machine.system()

if host_system == 'windows' or host_system == 'cygwin'
  if host_cpu_family == 'x86'
    cflags += '-mstackrealign'
    ldflags += '-Wl,--kill-at'
  endif
endif

cc = meson.get_compiler('cpp')


sources = [
  'src/DupBlocks.cpp',
  'src/RestoreMotionBlocks.cpp',
  'src/SCSelect.cpp',
  'src/shared.cpp',
  'src/RemoveDirt.cpp',
]

deps = [
  dependency('vapoursynth').partial_dependency(
      includes: true,
      compile_args: true),
]

shared_module('removedirt',
              sources,
              dependencies: deps,
              link_args: ldflags,
              cpp_args: cflags,
              install: true)
