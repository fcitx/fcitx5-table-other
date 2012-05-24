set(DEPRECATED_TABLE_NAMES
bn/bengali-inscript # can be deprecated by m17n and keyboard layout
bn/bengali-probhat # can be deprecated by m17n and keyboard layout
gu/gujarati-inscript # can be deprecated by m17n
gu/gujarati-phonetic # can be deprecated by m17n
hi/hindi-inscript # can be deprecated by m17n
hi/hindi-phonetic # can be deprecated by m17n
kn/kannada-inscript # can be deprecated by m17n
kn/kannada-kgp # can be deprecated by m17n
ml/malayalam-inscript # can be deprecated by m17n
ne/nepali-rom # can be deprecated by m17n
ne/nepali-trad # can be deprecated by m17n
pa/punjabi-inscript # can be deprecated by m17n
pa/punjabi-jhelum # can be deprecated by m17n
pa/punjabi-phonetic # can be deprecated by m17n
ta/tamil-inscript # can be deprecated by m17n
ta/tamil-phonetic # can be deprecated by m17n
te/telugu-inscript # can be deprecated by m17n
)

set(TABLE_NAMES
am/amharic
ar/arabic
ml/malayalam-phonetic
ta/tamil-remington
other/cns11643
other/compose
other/emoji
other/ipa-x-sampa
other/latex
uk/translit-ua
ru/rustrad
ru/translit
ru/yawerty
th/thai
vi/viqr
)

if (ENABLE_DEPRECATED)
set(TABLE_NAMES ${TABLE_NAMES} ${DEPRECATED_TABLE_NAMES})
endif (ENABLE_DEPRECATED)

set(MB_FILE)
set(CONF_FILE)

foreach(table ${TABLE_NAMES})

    string(REGEX REPLACE "^([a-z]+)/.+" "\\1"  TABLE_DIR "${table}")
    string(REGEX REPLACE "^[a-z]+/(.+)" "\\1" TABLE_NAME "${table}")
    intltool_merge_translation(${CMAKE_CURRENT_SOURCE_DIR}/${table}.conf.in ${CMAKE_CURRENT_BINARY_DIR}/${TABLE_NAME}.conf )

    add_custom_command(OUTPUT ${TABLE_NAME}.mb
                       DEPENDS ${table}.txt
                       COMMAND ${TXT2MB} ARGS ${CMAKE_CURRENT_SOURCE_DIR}/${table}.txt ${CMAKE_CURRENT_BINARY_DIR}/${TABLE_NAME}.mb)

    set(MB_FILE ${MB_FILE} ${CMAKE_CURRENT_BINARY_DIR}/${TABLE_NAME}.mb)
    set(CONF_FILE ${CONF_FILE} ${CMAKE_CURRENT_BINARY_DIR}/${TABLE_NAME}.conf)
endforeach(table ${TABLE_NAMES})

add_custom_target(table_data ALL DEPENDS ${MB_FILE} ${CONF_FILE})

install(FILES ${CONF_FILE} DESTINATION ${FCITX4_PREFIX}/share/fcitx/table)
install(FILES ${MB_FILE} DESTINATION ${FCITX4_PREFIX}/share/fcitx/table)