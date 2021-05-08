
includes = [include_directories('../include')]

sources = ['async.cpp',
           'cfg.cpp',
           'color_sinks.cpp',
           'file_sinks.cpp',
           'fmt.cpp',
           'spdlog.cpp',
           'stdout_sinks.cpp']

common_cpp_args += ['-DSPDLOG_COMPILED_LIB']

if build_machine.system() == 'windows'
    # https://stackoverflow.com/questions/5207765/c4275-warning-in-visual-studio
    # https://docs.microsoft.com/en-us/cpp/error-messages/compiler-warnings/compiler-warning-level-1-c4251?view=msvc-160
    specific_cpp_args += ['/wd4251', '/wd4275']
endif


if lib_type == 'static' or lib_type == 'both'
    static_lib_name        = name
    static_lib_name_prefix = []
    static_lib_name_suffix = []

    if system == 'windows' and cppc_id == 'msvc'
        static_lib_name       += '_static'
        static_lib_name_prefix = ''
        static_lib_name_suffix = 'lib'
    endif

    spdlog_static = static_library(static_lib_name,
                                  name_prefix         : static_lib_name_prefix,
                                  name_suffix         : static_lib_name_suffix,
                                  include_directories : includes,
                                  sources             : sources,
                                  cpp_args            : common_cpp_args + specific_cpp_args,
                                  link_args           : link_args,
                                  install             : true)

    spdlog_static_dep = declare_dependency(include_directories : includes,
                                           compile_args        : common_cpp_args,
                                           link_with           : spdlog_static)
endif

if lib_type == 'shared' or lib_type == 'both'
    shared_lib_name = name

    spdlog_shared = shared_library(shared_lib_name,
                                  include_directories : includes,
                                  sources             : sources,
                                  cpp_args            : common_cpp_args + specific_cpp_args + ['-DSPDLOG_SHARED_LIB', '-Dspdlog_EXPORTS', '-DFMT_EXPORT', '-DFMT_SHARED'],
                                  link_args           : link_args,
                                  install             : true)

    spdlog_shared_dep = declare_dependency(include_directories : includes,
                                           compile_args        : common_cpp_args + ['-DSPDLOG_SHARED_LIB', '-DFMT_SHARED'],
                                           link_with           : spdlog_shared)
endif


if lib_type == 'static'
    spdlog_dep = spdlog_static_dep
elif lib_type == 'shared' or lib_type == 'both'
    spdlog_dep = spdlog_shared_dep
endif
