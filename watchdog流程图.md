# 流程图

![图片](work/image.png)


# 寄存器

```c++
1.WDR_CR中 0 bit 表示是否是能，1 bit 表示超时进中断还是直接重启 [2:4] bits 表示 pclk cycles,[5:31]表示 Reserved
2.WDT_TORR中[31:8]表示 Reserved，[7:4]表示TOP_INIT(first timeout init)，[3:0] 表示 TOP(restart set counter)
3. WDT_CVRR中[0:WDT_CNT_WIDTH]表示WDT Current Counter Value Register，[WDT_CNT_WIDTH:31]表示 Reserved
4.WDT_CRR中[0:7]表示Counter Restart Register Values:0x76 (RESTART): Watchdog timer restart command，[8:31] 表示 Reserved
5.WDT_STAT中 0 bit表示Interrupt status register0x0 (INACTIVE): Interrupt is inactive 0x1 (ACTIVE): Interrupt is active regardless of polarity，[1:31] 表示 Reserved
6. WDT_EIO中 0 bit 表示Interrupt Clear Register，[1:31] 表示 Reserved
//wdt_register.h
#include "int_type.h"

// base addr 
#define  WDT_REG_BASE    0x15500000

// TODO : WDT_CNT_WIDTH wait to get
#define WDT_CNT_WIDTH    0x10

/* Watchdog timer control register (WDT_CR) */
#define WDT_CR (*(volatile WDT_CR_reg*)(WDT_REG_BASE + 0x00))

/* Watchdog timer timeout range register (WDT_TORR) */
#define WDT_TORR (*(volatile WDT_TORR_reg*)(WDT_REG_BASE + 0x04))

/* Watchdog timer current count value register (WDT_CCVR) */
#define WDT_CCVR (*(volatile WDT_CCVR_reg*)(WDT_REG_BASE + 0x08))

/* Watchdog timer control register (WDT_CRR) */
#define WDT_CRR (*(volatile WDT_CRR_reg*)(WDT_REG_BASE + 0x0C))

/* Watchdog timer interrupt status register (WDT_STAT) */
#define WDT_STAT (*(volatile WDT_STAT_reg*)(WDT_REG_BASE + 0x10))

/* Watchdog timer end of interrupt register (WDT_EOI) */
#define WDT_EOI (*(volatile WDT_EOI_reg*)(WDT_REG_BASE + 0x14))

typedef struct {
    volatile uint32_t WDT_CR;
    volatile uint32_t WDT_TORR;
    volatile uint32_t WDT_CCVR;
    volatile uint32_t WDT_CRR;
    volatile uint32_t WDT_STAT;
    volatile uint32_t WDT_EOI;
} wdt_regs_t;



```



