rkr7_patches4补丁说明：
lyx@ubuntu:~/rk3566-11-eink/RKDocs/android/patches/ebook/rkr7_patchs4$ tree
.
├── device
│   └── rockchip
│       └── rk356x
│           └── 0001-sepolicy_ebook-add-property-sys.diff.percent.patch      //增加sys.diff.percent属性，设置全刷比例，根据前后帧的差异比决定是否全刷，0不生效，有效值1到100
├── hardware
│   └── rockchip
│       └── hwcomposer
│           └── einkhwc
│               ├── 0001-einkcompositorworker-add-waveform-check.patch      //增加波形文件版本号识别，避免4bit的波形文件启用regal模式
│               ├── 0002-add-diff-percent-check.patch                       //增加sys.diff.percent属性功能
│               └── 0003-fix-force-full-twice-under-regal-mode.patch        //解决regal模式下force full会全刷两次问题
│               ├── 0004-update-for-new-ebc.patch		//此版本开始不在支持Y8 buf，有需要的单独找RK；增加sys.eink.waiting.time属性用于设置帧等待时间，对于一些点击切换页面的场景，通过设置这个时间，单位ms，可以提升响应速度，默认关闭该功能；
│               ├── 0005-revert-skip-count-set-when-suspend-and-resume.patch  //解决刚唤醒的前几帧，刷新率低问题
│               ├── 0006-Revert-fix-weifeng-color-panel.patch	//revert威锋彩屏的算法代码，保留原来的。
│               └── 0007-Eink-every-frame-update-must-ensure-that-there-is-an.patch		//避免唤醒时概率性先显示系统图像再显示锁屏密码界面
├── kernel
│   ├── 0001-drm-rockchip-ebc_dev-release-version-v2.27.patch
│   ├── 0002-drm-rockchip-ebc_dev-release-version-v2.28.patch
│   ├── 0003-drm-rockchip-ebc_dev-release-version-v3.00.patch
│   ├── 0004-arm64-dts-rockchip-update-wacom-touch-i2c-clock-freq.patch
│   ├── 0005-arm64-dts-rk3566-eink-update-gpu-opp-table.patch
│   ├── 0006-drm-rockchip-ebc_dev-release-version-v3.01.patch
│   ├── 0007-drm-rockchip-ebc_dev-release-version-v3.02.patch
│   ├── 0008-drm-rockchip-ebc_dev-release-version-v3.03.patch
│   ├── 0009-drm-rockchip-ebc_dev-release-version-v3.04.patch
│   ├── 0010-drm-rockchip-ebc_dev-release-version-v3.05.patch     //ebc驱动及相关更新，提高手写速度，提升响应速度等
│   ├── 0011-drivers-input-sensor-dev-support-wakeup.patch        //sensor架构更新，支持lite唤醒
│   └── 0012-drivers-input-gsensor-mxc6655xa-support-orientation-.patch    //gsensor mxc6655xa驱动更新，支持lite旋转唤醒
│   ├── 0013-drm-rockchip-ebc_dev-tps65185-clear-shadow-when-resu.patch  //解决部分屏唤醒后tps65185电源异常
│   ├── 0014-drm-rockchip-ebc_dev-release-version-4.00.patch
│   ├── 0015-drm-rockchip-ebc_dev-release-version-v4.01.patch
│   ├── 0016-drm-rockchip-ebc_dev-release-version-v4.02.patch
│   ├── 0017-drm-rockchip-ebc_dev-release-version-v4.03.patch
│   ├── 0018-drm-rockchip-ebc_dev-release-version-v4.04.patch
│   └── 0019-drm-rockchip-ebc_dev-release-version-v4.05.patch    //ebc驱动及相关更新，调整一些代码架构；优化手写模式下的背景更新残影严重问题，优化手写模式下背景更新控制机制；待机下的logo图片更新采用part模式；
│   └── 0020-drm-rockchip-ebc_dev-release-version-v4.06.patch    //增加dts配置，panel,disable_logo, 用于关闭rk的待机和关机logo机制，使用客户自己的logo显示机制
│   ├── 0021-drm-rockchip-ebc_dev-release-version-v4.07.patch   //增加overlay状态获取，通过ioctl获取驱动的overlay状态，int overlay_status; ioctl(ebc_fd, EBC_GET_OVERLAY_STATUS, &overlay_status)；0：disable  1: enable
│   └── 0022-drm-rockchip-ebc_dev-release-version-v4.08.patch   //增加overlay模式下的背景更新控制，通过ioctl控制，使能控制：ioctl(ebc_fd, EBC_ENABLE_BG_CONTROL, NULL)；关闭控制：ioctl(ebc_fd, EBC_DISABLE_BG_CONTROL, NULL)；
						     //默认是使能控制的，这样overlay模式下，背景的更新机制与非overlay模式下一致；关闭控制后，背景更新会更快，类似auto模式；
├── packages
│   └── apps
│       └── NoteDemo //手写应用更新，提升手写速度，解决待机cpu占用率高问题，解决闪退问题
│           ├── 0001-fix-unmmap-err.patch
│           ├── 0002-paintworker-improve-handwrite-speed-add-latency-log.patch
│           ├── 0003-paintwork-fix-issue-paintworker-routine-function-cau.patch
│           ├── 0004-Some-code-sorting.patch
│           ├── 0005-NoteDemo-fix-app-crash-by-initFlag-always-true-after.patch
│           ├── 0006-NoteDemo-fix-memory-leak.patch
├── rkbin
│   ├── 0001-rk3566-ddr-update-ultra-ddr-bin-to-v1.10.patch  //更新ultra稳定性问题，修复部分lpddr4x颗粒稳定性问题
│   └── 0002-rk3566-bl31-ultra-update-version-to-v2.12.patch //解决ultra唤醒背光闪问题，需要同时修改硬件，没有背光功能的不受影响
└── u-boot
    ├── 0001-drivers-rk_eink-add-more-waveform-version-for-pvi.patch  //支持更多版本的波形文件
    ├── 0002-configs-rk3566-eink-enable-CONFIG_GPIO_KEY.patch    //开启gpio key功能
    └── 0003-video-rk_ebc-revert-DSP_HS_END-2-to-fix-XLE-on-delay.patch  //修复时序问题

       13 directories, 41 files

--------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------
rkr7_patches3补丁说明：
lyx@ubuntu:~/rk3566-11-eink/RKDocs/android/patches/ebook/rkr7_patchs3$ tree
.
├── device
│   └── rockchip
│       └── common
│           └── 0001-sepolicy-allow-proc-for-bluetooth.patch 蓝牙权限相关补丁，解决因权限问题导致的蓝牙功耗异常
├── hardware
│   └── broadcom
│       └── libbt
│           └── 0001-BT-broadcom-fix-bt-wake-gpio-control.patch  蓝牙权限相关补丁，解决因权限问题导致的蓝牙功耗异常
└── kernel
    ├── 0001-drm-rockchip-ebc_dev-release-version-v2.23.patch    ebc驱动补丁，解决overlay的lut模式无法指定问题
    ├── 0002-drm-rockchip-ebc_dev-release-version-v2.24.patch    ebc驱动补丁，解决手写死机问题
    ├── 0003-drm-rockchip-dev_ebc-release-version-v2.25.patch    ebc驱动补丁，优化手写过程的背景更新机制，避免手写卡顿问题
    └── 0004-drm-rockchip-dev_ebc-release-version-v2.26.patch    ebc驱动补丁，优化手写算法，大大降低手写功耗

7 directories, 6 files
--------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------
rkr7_patches2补丁说明：

lyx@ubuntu:~/rk3566-11-eink/RKDocs/android/patches/ebook/rkr7_patchs2$ tree
.
├── bootable
│   └── recovery
│       └── 0001-eink-minui-update-to-match-kernel-defined.patch   更新结构体定义，与最新的kernel ebc驱动匹配
│       └── 0002-eink-minui-update-ebc-buf-info-with-kernel-define.patch  更新结构体定义，与最新的kernel ebc驱动匹配，使用tid_name标识用户，用于ebc buf管理，避免因为应用异常退出导致ebc_buf流失
├── device
│   └── rockchip
│       └── rk356x
│           ├── 0001-rk3566-eink-use-gamma-property-to-do-contrast-contro.patch    新对比度调节方法相关补丁
│           ├── 0002-rk3566_eink-build-64bit-android-platform.patch                编译64位的android系统，与此前提供的64bit补丁一致，需要64bit系统的可以选择打上，否则忽略；
│           └── 0003-rk3566-eink-enable-Disk-encryption.patch                      打开磁盘加密，可以提高antutu跑分，对实际性能没有影响，新项目可以考虑打上补丁；
                                                                                   由于补丁改变了磁盘数据格式，旧项目之前没有使能磁盘加密的，现在打开的话，ota会失败，不建议旧项目使用；
├── frameworks
│   ├── base
│   │   └── 0001-EINK-use-new-way-to-control-Contrast.patch                        新对比度调节方法相关补丁
│   │   ├── 0002-Add-the-mAppDpiMapLock-to-avoid-causing-the-BadParce.patch        第三方应用调节功能，增加锁保护
│   │   └── 0003-Eink-fix-some-err-in-app-custom-function.patch                    修复一些应用异常导致android反复重启的问题
│   └── native
│       └── 0001-Feature-Support-Gamma-calibration.patch                           新对比度调节方法相关补丁
├── hardware
│   └── rockchip
│       └── hwcomposer
│           └── einkhwc
│               ├── 0001-use-debug.sf.gamma.gamma-to-do-contrast-control-on-S.patch   新对比度调节方法相关补丁
│               ├── 0002-Remove-unnecessary-include-mali_gralloc_formats.h-an.patch   去除无用代码
│               ├── 0003-hwc_adajust_sf_vsync-fix-vsync-count-maybe-always-29.patch   解决唤醒后，系统概率变慢问题
│               ├── 0004-fix-weifeng-color-panel.patch                                威锋彩屏补丁
│               ├── 0005-DrmEink-Solve-the-risk-of-a-null-pointer-exception.patch     规避极低概率的空指针问题
│               ├── 0006-fix-Rgb888ToGray16ByRga-when-logo-display.patch              解决logo显示时灰度损失问题
│               ├── 0007-support-regal-mode-for-eink-panel.patch                      支持元太regal去残影功能，需要元太libeink.so和5bit波形文件支持，只有GLR和GLD模式支持regal刷新
│               ├── 0008-regal-use-y4-commit-to-do-out-regal-mode.patch               regal相关补丁
│               └── 0009-fix-resume-failed-by-regal-mode.patch                        regal相关补丁
│               └── 0010-out-regal-mode-no-need-to-do-force-full.patch                regal相关补丁
│               └── 0011-update-ebc_buf-info.patch                                    更新结构体定义，与最新的kernel ebc驱动匹配，使用tid_name标识用户，用于ebc buf管理，避免因为应用异常退出导致ebc_buf流失
├── kernel
│   ├── 0001-mfd-rk808-disable-rk817-int-when-shutdown.patch                          更新rkr7_patches中的补丁0007-drivers-mfd-rk808-disable-rk817-int-when-shutdown.patch
│   ├── 0002-drm-rockchip-ebc_dev-release-version-v2.13.patch                         ebc驱动更新，解决EPD_AUTO刷新不全问题
│   ├── 0003-drm-rockchip-ebc_dev-release-version-v2.14.patch                         ebc驱动更新，过滤唤醒时的黑帧
│   ├── 0004-arm64-dts-rockchip-rk3566-eink-reserve-ebc-framebuff.patch               regal相关补丁，增大framebuff size，支持regal模式
│   ├── 0005-drm-rockchip-ebc_dev-release-version-v2.15.patch                         regal相关补丁，ebc驱动更新，支持regal 5bit波形文件
│   ├── 0006-drm-rockchip-ebc_dev-release-version-v2.16.patch                         regal相关补丁，ebc驱动更新，解决regal的个别问题
│   └── 0007-drm-rockchip-ebc_dev-release-version-v2.17.patch                         regal相关补丁，ebc驱动更新，解决regal的个别问题
│   ├── 0008-drm-rockchip-ebc_dev-release-version-v2.18.patch                         regal相关补丁，ebc驱动更新，AUTO模式支持Y8数据
│   ├── 0009-arm64-dts-rockchip-rk3566-rk817-eink-w103-assign-ebc.patch               ebc dclk补丁，可以更精确的分配到sdclk
│   ├── 0010-drm-rockchip-ebc_tcon-set-ebc-dclk-div-0.patch                           ebc dclk补丁，可以更精确的分配到sdclk
│   ├── 0011-drm-rockchip-ebc_dev-release-version-v2.19.patch                         ebc驱动更新,auto模式刷新不全问题
│   ├── 0012-drm-rockchip-ebc_dev-release-version-v2.20.patch                         ebc驱动更新，ebc有buf请求时提前poweron
│   ├── 0013-drm-rockchip-ebc_dev-release-version-v2.21.patch                         ebc驱动更新，ebc延迟200ms下电，减少一些场景下的频繁上下电问题
│   └── 0014-arm64-dts-rockchip-config-the-pmic_sleep-internal-pu.patch               pmic sleep配置更新
│   └── 0015-drm-rockchip-ebc_dev-release-version-v2.22.patch                         ebc驱动更新,使用tid_name标识用户，用于ebc buf管理，避免因为应用异常退出导致ebc_buf流失
├── packages
│   └── apps
│       └── NoteDemo
│           └── 0001-paintworker-update-to-match-kernel-defined.patch                 更新结构体定义，与最新的kernel ebc驱动匹配
│           └── 0002-update-ebc-buf_info-with-kernel-defined.patch                    更新结构体定义，与最新的kernel ebc驱动匹配，使用tid_name标识用户，用于ebc buf管理，避免因为应用异常退出导致ebc_buf流失
├── rkbin
│   ├── 0001-rk3566-bl31-ultra-update-version-to-v2.10.patch                          bl31 bin更新，稳定性与功耗相关问题
│   ├── 0002-rk3566-ddr-update-ultra-ddr-bin-to-v1.09.patch                           ddr bin更新，稳定性与功耗相关问题
│   └── 0003-rk3566-bl31-ultra-update-version-to-v2.11.patch                          bl31 bin更新，解决v2.10 bl31 bin唤醒变慢的问题
└── u-boot
    └── 0001-rk_ebc_tcon-set-ebc-dclk.patch                                           ebc dclk补丁，可以更精确的分配到sdclk

18 directories, 41 files

--------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------
rkr7_patches补丁说明：

lyx@ubuntu:~/rk3566-11-eink/RKDocs/android/patches/ebook$ tree
.
├── 0001-arm64-dts-rk3566-rk817-eink-w103-add-backlight-suppo.patch  添加背光功能，可参考此补丁
├── 0001-drivers-input-sensor-hall-sensor-mh248-support-ebook.patch     添加皮套（hall）唤醒功能，需要打这个补丁
├── 0001-rk3566_eink-build-64bit-android-platform.patch   如果要编译64位android，需要打此补丁
└── rkr7_patchs  该目录下的补丁是基于android-11.0-ebook-rkr7版本的必要补丁包
    ├── bootable
    │   └── recovery
    │       ├── 0001-install-Support-early-loader-upgrade-method.patch  支持rk loader ota升级补丁1
    │       └── 0002-Optimize-error-handling.patch  支持rk loader ota升级补丁2
    ├── build
    │   └── make
    │       └── core
    │           └── 0001-build-Add-upgrading-logo.patch  支持logo分区ota升级补丁1
    ├── device
    │   └── rockchip
    │       ├── common
    │       │   ├── 0001-chmod-dev-waveform-for-ebook.patch  支持元太regal模式补丁1
    │       │   ├── 0002-Add-upgrading-logo-feature.patch 支持logo分区ota升级补丁2
    │       │   └── 0003-A-B-support-logo-for-ebook.patch 支持logo分区ota升级补丁3
    │       └── rk356x
    │           ├── 0001-rk3566_eink-add-dir-resolution-for-app-preinstall-fu.patch  增加APK预置目录
    │           ├── 0002-rk3566-eink-disable-autoPowerModes.patch  可选非必要补丁，关闭autoPowerMode，减少待机时的后台唤醒次数
    │           ├── 0003-ebook-add-dev-waveform-sepolicy.patch   支持元太regal模式补丁2
    │           ├── 0004-rk356x-support-logo-upgrade-for-ebook.patch  支持logo分区ota升级补丁4
    │           └── 0005-rk3566_eink-A-B-pamameter-logo-logo_a-logo_b-to-supp.patch  支持logo分区ota升级补丁5
    ├── frameworks
    │   └── base
    │       ├── 0001-Eink-make-set-api-dpi-function-only-effect-activity.patch  DPI调节补丁1
    │       ├── 0002-Eink-Filter-RockVideoPlayer-apk-from-its-packagename.patch  过滤RockVideoPlayer apk，不参与DPI，模式的调节
    │       └── 0003-Eink-replace-some-methods-name-to-avoid-same-name-fr.patch  DPI调节补丁2
    │       └── 0004-EinkManager-add-EPD_AUTO_DU-and-EPD_AUTO_DU4-mode.patch  增加EPD_AUTO_DU和EPD_AUTO_DU4模式补丁1
    │       └── 0005-Eink-Realize-the-DPI-setting-in-App-level-and-solve-.patch  修改DPI方案，解决已知的一些问题
    ├── hardware
    │   ├── interfaces
    │   │   └── 0001-health-wakeup-per-30-minutes-when-no-charging-to-red.patch  可选非必要补丁，可减少healthd待机时的后台唤醒次数
    │   └── rockchip
    │       └── hwcomposer
    │           └── einkhwc
    │               ├── 0001-support-color-eink1.patch  支持元太彩屏补丁，具体屏需要找元太要彩色算法库，并替换次补丁中的库
    │               ├── 0002-support-eink-regal-mode-use-eink-so.patch  支持元太regal模式补丁3，具体屏需要找元太要regal算法库和相应的波形文件
    │               ├── 0003-add-FALLTHROUGH_INTENDED-to-fix-build-err.patch  修复编译错误
    │               └── 0004-adjust-vsync-when-suspend-and-resume-to-avoid-screen.patch  休眠唤醒概率性显示异常（多为黑屏）补丁
    │               └── 0005-add-EPD_AUTO_DU-and-EPD_AUTO_DU4-mode.patch 增加EPD_AUTO_DU和EPD_AUTO_DU4模式补丁2
    ├── kernel
    │   ├── 0001-drm-rockchip-ebc_dev-release-version-v2.09.patch  墨水屏驱动补丁1，支持多颗墨水屏pmic兼容补丁1
    │   ├── 0002-drm-rockchip-ebc_dev-release-version-v2.10.patch  墨水屏驱动补丁2，auto模式增加锁保护
    │   ├── 0003-regulator-xz3216-add-mode-setting-support.patch  DCDC xz3216驱动补丁1，支持模式设置
    │   ├── 0004-drm-rockchip-ebc_dev-release-version-v2.11.patch  支持元太regal模式补丁3，墨水屏驱动补丁3，增加/dev/waveform节点
    │   └── 0005-regulator-xz3216-add-resume-function.patch  DCDC xz3216驱动补丁2，解决reboot死机问题
    │   └── 0006-drm-rockchip-ebc_dev-release-version-v2.12.patch 增加EPD_AUTO_DU和EPD_AUTO_DU4模式补丁3，墨水屏驱动补丁4
    │   └── 0007-drivers-mfd-rk808-disable-rk817-int-when-shutdown.patch 解决关机过程频繁按power键导致系统死机问题
    ├── rkbin
    │   ├── 0001-rk3568-bl31-update-version-to-v2.08.patch  修复待机概率性系统重启问题
    │   └── 0002-rk3568-bl31-update-version-to-v2.09.patch  修复待机概率性功耗不对问题
    ├── RKTools
    │   └── 0001-pack-logo_a-and-logo_b.patch 支持logo分区ota升级补丁6
    └── u-boot
        └── 0001-drivers-video-rk_eink-support-multi-pmics-define.patch 支持多颗墨水屏pmic兼容补丁2
        └── 0002-configs-rk3566-eink.config-enable-gpio-leds.patch   uboot增加led灯的支持

21 directories, 38 files
