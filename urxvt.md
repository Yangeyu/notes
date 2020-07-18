
!!--------------------xdefauls
!!窗口大小及标题设置
!!URxvt.geometry:  85x20+60+80
!!URxvt.title:lepoke-rxvt-unicode

URxvt.font: xft:CodeNewRoman Nerd Font Mono:pixelsize=22
urxvt*scrollBar: false
.transparent: false
!!不知道是什么设置
URxvt*geometry: 90x28
!!字体间距
URxvt.letterSpace:0

Xft*dpi: 96
Xft*antialias: true
Xft*hinting: true
Xft*hintstyle: hintfull
Xft*rgba: rgb
*internalBorder: 23
URxvt*fading: 0
URxvt*tintColor: #ffffff
URxvt*shading: 0
URxvt*inheritPixmap: False
URxvt*background: #4B414C

!!颜色设置
URxvt.depth:32
URxvt.background:[75]#272938

URxvt*color0:#2E3436
URxvt*color1:#CC0000
URxvt*color2:#8DE4A3
URxvt*color3:#C4A000
URxvt*color4:#2B79DC
URxvt*color5:#D455E9
URxvt*color6:#059FA2
URxvt*color7:#D3D7CF
URxvt*color8:#555753
URxvt*color9:#EF2929
URxvt*color10:#37EF65
URxvt*color11:#FCE94F
URxvt*color12:#BA9CFF
URxvt*color13:#AD7FA8
URxvt*color14:#34E2E2
URxvt*color15:#EEEEEC
URxvt.foreground:#ffffff

!!禁用Ctrl+shift
URxvt.iso14755: false
URxvt.iso14755_52: false
!!URL操作
!!URxvt.urlLauncher:google-chrome
URxvt.url-select.launcher: /home/yang/.config/urxvt
URxvt.perl-ext-common: default,matcher
URxvt.matcher.button: 1
URxvt.keysym.C-Delete: perl:matcher:last
URxvt.keysym.M-Delete: perl:matcher:list
URxvt.perl-ext: default,url-select
URxvt.url-select.underline: true

!!闪烁光标
!!URxvt.cursorBlink: true
!!光标为下划线
URxvt.cursorUnderline: true
