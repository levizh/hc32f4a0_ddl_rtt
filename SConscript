import rtconfig
from building import *

# get current directory
cwd = GetCurrentDir()

# export the packages directory
PACKAGES_PATH = cwd
Export('PACKAGES_PATH')

# The set of source files associated with this SConscript file.

src = Split('''
cmsis/Device/HDSC/hc32f4xx/Source/system_hc32f4a0.c
hc32_ll_driver/src/hc32_ll.c
hc32_ll_driver/src/hc32_ll_aos.c
hc32_ll_driver/src/hc32_ll_clk.c
hc32_ll_driver/src/hc32_ll_dma.c
hc32_ll_driver/src/hc32_ll_efm.c
hc32_ll_driver/src/hc32_ll_fcg.c
hc32_ll_driver/src/hc32_ll_gpio.c
hc32_ll_driver/src/hc32_ll_icg.c
hc32_ll_driver/src/hc32_ll_interrupts.c
hc32_ll_driver/src/hc32_ll_pwc.c
hc32_ll_driver/src/hc32_ll_rmu.c
hc32_ll_driver/src/hc32_ll_sram.c
hc32_ll_driver/src/hc32_ll_utility.c
hc32_ll_driver/src/hc32f4a0_ll_interrupts_share.c
''')

if GetDepend(['BSP_USING_NAND']):
    src += ['hc32_ll_driver/src/hc32_ll_nfc.c']

if GetDepend(['BSP_USING_SDRAM']):
    src += ['hc32_ll_driver/src/hc32_ll_dmc.c']

if GetDepend(['RT_USING_SERIAL']):
    src += ['hc32_ll_driver/src/hc32_ll_usart.c']
    src += ['hc32_ll_driver/src/hc32_ll_tmr0.c']

if GetDepend(['RT_USING_I2C']):
    src += ['hc32_ll_driver/src/hc32_ll_i2c.c']

if GetDepend(['RT_USING_SPI']):
    src += ['hc32_ll_driver/src/hc32_ll_spi.c']

if GetDepend(['RT_USING_QSPI']):
    src += ['hc32_ll_driver/src/hc32_ll_qspi.c']

if GetDepend(['RT_USING_CAN']):
    src += ['hc32_ll_driver/src/hc32_ll_can.c']

if GetDepend(['BSP_USING_ETH']):
    src += ['hc32_ll_driver/src/hc32_ll_eth.c']

if GetDepend(['RT_USING_ADC']):
    src += ['hc32_ll_driver/src/hc32_ll_adc.c']

if GetDepend(['RT_USING_DAC']):
    src += ['hc32_ll_driver/src/hc32_ll_dac.c']

if GetDepend(['RT_USING_RTC']):
    src += ['hc32_ll_driver/src/hc32_ll_rtc.c']

if GetDepend(['RT_USING_WDT']):
    src += ['hc32_ll_driver/src/hc32_ll_swdt.c']
    src += ['hc32_ll_driver/src/hc32_ll_wdt.c']

if GetDepend(['RT_USING_SDIO']):
    src += ['hc32_ll_driver/src/hc32_ll_sdioc.c']

if GetDepend(['RT_USING_ON_CHIP_FLASH']):
    src += ['hc32_ll_driver/src/hc32_ll_efm.c']

if GetDepend(['RT_USING_HWTIMER']):
    src += ['hc32_ll_driver/src/hc32_ll_tmr2.c']
    src += ['hc32_ll_driver/src/hc32_ll_tmr4.c']
    src += ['hc32_ll_driver/src/hc32_ll_tmr6.c']
    src += ['hc32_ll_driver/src/hc32_ll_tmra.c']

if GetDepend(['RT_USING_PULSE_ENCODER']):
    src += ['hc32_ll_driver/src/hc32_ll_tmr6.c']
    src += ['hc32_ll_driver/src/hc32_ll_tmra.c']

if GetDepend(['RT_USING_PWM']):
    src += ['hc32_ll_driver/src/hc32_ll_tmr4.c']
    src += ['hc32_ll_driver/src/hc32_ll_tmr6.c']
    src += ['hc32_ll_driver/src/hc32_ll_tmra.c']

if GetDepend(['RT_USING_INPUT_CAPTURE']):
    src += ['hc32_ll_driver/src/hc32_ll_tmr6.c']

if GetDepend(['RT_HWCRYPTO_USING_RNG']):
    src += ['hc32_ll_driver/src/hc32_ll_trng.c']

if GetDepend(['RT_HWCRYPTO_USING_CRC']):
    src += ['hc32_ll_driver/src/hc32_ll_crc.c']

if GetDepend(['RT_HWCRYPTO_USING_AES']):
    src += ['hc32_ll_driver/src/hc32_ll_aes.c']

if GetDepend(['RT_HWCRYPTO_USING_SHA2']):
    src += ['hc32_ll_driver/src/hc32_ll_hash.c']

if GetDepend(['BSP_USING_USBD']) or GetDepend(['BSP_USING_USBH']):
    src += ['hc32_ll_driver/src/hc32_ll_usb.c']

if GetDepend(['BSP_RTC_USING_XTAL32']) or GetDepend(['RT_USING_PM']):
    src += ['hc32_ll_driver/src/hc32_ll_fcm.c']

path = [
    cwd + '/cmsis/Device/HDSC/hc32f4xx/Include',
    cwd + '/cmsis/Include',
    cwd + '/hc32_ll_driver/inc',]

CPPDEFINES = ['USE_DDL_DRIVER']

group = DefineGroup('Libraries', src, depend = [''], CPPPATH = path, CPPDEFINES = CPPDEFINES)

start_src = []
if rtconfig.PLATFORM in ['gcc']:
    start_src += [cwd + '/cmsis/Device/HDSC/hc32f4xx/Source/GCC/startup_hc32f4a0.S']
elif rtconfig.PLATFORM in ['armcc', 'armclang']:
    start_src += [cwd + '/cmsis/Device/HDSC/hc32f4xx/Source/ARM/startup_hc32f4a0.s']
elif rtconfig.PLATFORM in ['iccarm']:
    start_src += [cwd + '/cmsis/Device/HDSC/hc32f4xx/Source/IAR/startup_hc32f4a0.s']

DefineGroup('Drivers', start_src, depend = [''], CPPPATH = path)

Return('group')
