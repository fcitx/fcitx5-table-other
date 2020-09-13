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

if(ENABLE_DEPRECATED)
  set(TABLE_NAMES ${TABLE_NAMES} ${DEPRECATED_TABLE_NAMES})
endif()

set(MB_FILES)
set(CONF_FILES)

foreach(table ${TABLE_NAMES})
  get_filename_component(table_name "${table}" NAME)
  fcitx5_translate_desktop_file("${table}.conf.in" "${table_name}.conf")
  set(mb_file "${CMAKE_CURRENT_BINARY_DIR}/${table_name}.main.dict")
  set(conf_file "${CMAKE_CURRENT_BINARY_DIR}/${table_name}.conf")

  add_custom_command(OUTPUT "${table_name}.main.dict"
    DEPENDS "${table}.txt"
    COMMAND LibIME::tabledict ARGS "${CMAKE_CURRENT_SOURCE_DIR}/${table}.txt"
    "${CMAKE_CURRENT_BINARY_DIR}/${table_name}.main.dict")

  set(MB_FILES ${MB_FILES} "${mb_file}")
  set(CONF_FILES ${CONF_FILES} "${conf_file}")
endforeach()

add_custom_target(table_data ALL DEPENDS ${MB_FILES})

install(FILES ${CONF_FILES} DESTINATION "${FCITX_INSTALL_PKGDATADIR}/inputmethod")
install(FILES ${MB_FILES} DESTINATION "${FCITX_INSTALL_PKGDATADIR}/table")
