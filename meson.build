project('teensy-meson-sample',
    version : '1.0',
    default_options : [
        'buildtype=minsize',
        'b_staticpic=false',
    ]
)

assert(meson.is_cross_build(), 'Teensy projects can only be built in a cross build environment.')

objcopy = find_program('objcopy') # Get objcopy
teensy_loader_cli = find_program('teensy-loader-cli') # Get teensy-loader-cli

# Teensy cores dep
cores = subproject('cores')

# Get teensy-core dep
teensy_core_dep = cores.get_variable('teensy_core_dep')

# Get mcu id
teensy_mcu = meson.get_cross_property('teensy_mcu')

# Get compiled object
blink_out = executable('blink', 'src/blink.cpp',
                       dependencies : teensy_core_dep,
                       link_args : ['-T' + cores.get_variable('ldscript')]
)

# Get flashable hex
blink_hex = custom_target('blink.hex',
                          input : blink_out,
                          output : 'blink.hex',
                          command : [objcopy, '-O', 'ihex', '-R', '.eeprom', '@INPUT@', '@OUTPUT@']
)

# Flash
run_target('flash',
           command : [teensy_loader_cli, '--mcu=' + teensy_mcu, '-v', '-w', blink_hex],
           depends : blink_out
)
