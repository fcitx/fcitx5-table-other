set(ICON24 fcitx-amharic.png fcitx-arabic.png)
set(ICON32 fcitx-thai.png)
set(ICON48 fcitx-compose.png fcitx-emoji.png fcitx-ipa-x-sampa.png
  fcitx-latex.png fcitx-rustrad.png fcitx-translit.png fcitx-translit-ua.png
  fcitx-yawerty.png fcitx-malayalam-phonetic.png fcitx-tamil-remington.png)
set(ICON64 fcitx-cns11643.png fcitx-viqr.png)

if(ENABLE_DEPRECATED)
  set(ICON48 ${ICON48} fcitx-bengali-inscript.png fcitx-bengali-probhat.png
    fcitx-gujarati-inscript.png fcitx-gujarati-phonetic.png
    fcitx-hindi-inscript.png fcitx-hindi-phonetic.png fcitx-kannada-inscript.png
    fcitx-kannada-kgp.png fcitx-malayalam-inscript.png fcitx-nepali.png
    fcitx-punjabi-inscript.png fcitx-punjabi-jhelum.png
    fcitx-punjabi-phonetic.png fcitx-tamil-inscript.png fcitx-tamil-phonetic.png
    fcitx-telugu-inscript.png)
endif()

foreach(icon ${ICON24} ${ICON32} ${ICON48} ${ICON64})
    string(REPLACE "fcitx-" "" icon_new ${icon})
    install(FILES ${icon} RENAME ${icon_new} DESTINATION share/fcitx/imicon)
endforeach()

install(FILES
    ${ICON32}
    DESTINATION share/icons/hicolor/32x32/apps)
install(FILES
    ${ICON48}
    DESTINATION share/icons/hicolor/48x48/apps)
install(FILES
    ${ICON64}
    DESTINATION share/icons/hicolor/64x64/apps)
