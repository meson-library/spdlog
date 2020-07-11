project('spdlog', ['cpp'],
         version       : '1.7.0',
         license       : ['MIT'],
         meson_version : '>= 0.49.0')




name = 'spdlog'




system     = build_machine.system()
cpu        = build_machine.cpu()
cpu_family = build_machine.cpu_family()

cppc    = meson.get_compiler('cpp')
cppc_id = cppc.get_id()

lib_type    = get_option('default_library')

includes  = []
sources   = []
cpp_args    = []
link_args = []




if system not in ['windows']
    error('Script (meson.build) not prepared for your platform yet.')
endif

if system == 'windows' and cppc_id not in ['msvc']
    error('Script (meson.build) not prepared for your compiler yet.')
endif




subdir('src')




if get_option('build_tests')
    if not meson.is_subproject()
        subdir('tests')
    else
        warning('The option ' + name + ':' + 'build_test' + ' not work in subproject.')
    endif
endif

if get_option('build_examples')
    if not meson.is_subproject()
        subdir('example')
    else
        warning('The option ' + name + ':' + 'build_examples' + ' not work in subproject.')
    endif
endif




install_subdir('include/spdlog',
               install_dir : 'include')

install_data(['LICENSE', 
              '3RDPARTYLICENSES.TXT'],
               rename : ['LICENSE.MIT', 
                         '3RDPARTYLICENSES.TXT'],
               install_dir :  'share/licenses/spdlog')
