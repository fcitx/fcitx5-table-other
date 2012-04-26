set(ICON32 fcitx-thai.png)
set(ICON48 fcitx-compose.png fcitx-emoji.png fcitx-ipa-x-sampa.png fcitx-latex.png fcitx-rustrad.png fcitx-translit.png fcitx-translit-ua.png fcitx-yawerty.png)
set(ICON64 fcitx-cns11643.png fcitx-viqr.png)

install(FILES
    ${ICON32}
    DESTINATION share/icons/hicolor/32x32/apps)
install(FILES
    ${ICON48}
    DESTINATION share/icons/hicolor/48x48/apps)
install(FILES
    ${ICON64}
    DESTINATION share/icons/hicolor/64x64/apps)