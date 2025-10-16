# DDR内存访问API文档

## 概述
通过MCU对DDR4和DDR5内存SPD的读写操作接口，通过串口(波特率：115200)使用JSON格式进行请求。

## 支持的操作
- 读取（read）
- 写入（write）
- 写保护（srswp）

## 参数说明

| 参数名  | 参数说明 |
|----|----|
| spdaddr | 设备地址范围：50-57 |
| type    | DDR内存类型，可选值：`ddr3`、`ddr4`、`ddr5` |
| cmd     | 操作类型，可选值：`read`、`write`、`srswp` |
| addr    | 操作的字节地址，以十六进制表示（如 `"0"`）    |
| value   |要写入的数据，以十六进制字符串表示，多个字节可连续拼接（如 `"AB12CD"`）|
| number  | 要读取的字节数量|

## 参数详解
- 如要读写 `ddr5` 128位寄存器或 `PMIC` 寄存器，则 `type` 修改为 `ddr3`；`PMIC` 地址为 `48`。
- `srswp` 设置写保护，`value` 全为`0`则解除所有`Block`写保护；`ddr3`仅支持解除写保护。
- `spdaddr` `type` `cmd` 为必填项，其他参数根据`cmd`填写。
- `addr` 仅`cmd`为`read` `write`时才需要填写。
- `number` 仅`cmd`为`read`时才需要填写。
- `value` 仅 `cmd` 为 `write`、`srswp` 时才需要填写。

### 1. 读取
向指定的字节地址读取数据，起始地址`00`，则从`00`开始读取三个字节。

**请求示例:**
```
{
  "spdaddr": "50",
  "type": "ddr5",
  "cmd": "read",
  "addr": "0",
  "value": "",
  "number": "3"  
}
```

**响应示例:**
```
AB12CD
```

### 2. 写入
向指定的字节地址写入数据，起始地址`0`，写入值`AB12CD`，则从`0`开始写入三个字节。

**请求示例:**
```
{
  "spdaddr": "50",
  "type": "ddr5",
  "cmd": "write",
  "addr": "0",
  "value": "AB12CD",
  "number": ""
}
```

**响应示例:**   

 - 待完善
```
无响应
```

### 3. 设置写保护

**DDR5请求示例:**
 - 设置写保护（`value` 由两组二位 16 进制值，转换为二进制对应 Block 位 `15 ~ 0`，`1` 为开启，`0` 为关闭）。

```
{
  "spdaddr": "50",
  "type": "ddr5",
  "cmd": "srswp",
  "addr": "",
  "value": "2233",
  "number": ""
}
```

**DDR4请求示例:**
 - 设置写保护（`value` 由二位 16 进制值取低四位，转换为二进制对应 Block 位 `3 ~ 0`，`1` 为开启，`0` 为关闭）。
 
```
{
  "spdaddr": "50",
  "type": "ddr4",
  "cmd": "srswp",
  "addr": "",
  "value": "0F",
  "number": ""
}
```

**响应示例:**
```
OK
```

**DDR3请求示例:**
 - 仅支持解除写保护
 
```
{
  "spdaddr": "50",
  "type": "ddr3",
  "cmd": "srswp",
  "addr": "",
  "value": "00",
  "number": ""
}
```


