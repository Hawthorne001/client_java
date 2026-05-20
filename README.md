# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-20T20:39:21Z
- **Commit:** [`8c254dd`](https://github.com/Hawthorne001/client_java/commit/8c254dd5ac96f1d53ffc4d59a163c5b1d19f9531)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.77K | ± 1.65K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.26K | ± 1.18K | ops/s | 1.1x slower |
| prometheusAdd | 62.85K | ± 1.15K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.74K | ± 149.55 | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 8.48K | ± 669.29 | ops/s | 8.9x slower |
| simpleclientInc | 7.95K | ± 76.55 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 7.62K | ± 36.54 | ops/s | 9.9x slower |
| simpleclientAdd | 7.56K | ± 519.28 | ops/s | 10x slower |
| openTelemetryInc | 6.40K | ± 1.25K | ops/s | 12x slower |
| openTelemetryAdd | 4.53K | ± 15.42 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 9.84K | ± 1.43K | ops/s | **fastest** |
| simpleclient | 5.63K | ± 46.33 | ops/s | 1.7x slower |
| prometheusNative | 4.03K | ± 145.12 | ops/s | 2.4x slower |
| openTelemetryClassic | 942.47 | ± 16.45 | ops/s | 10x slower |
| openTelemetryExponential | 745.58 | ± 46.78 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 35.43K | ± 281.11 | ops/s | **fastest** |
| openMetricsWriteToNull | 34.98K | ± 293.10 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 697.20K | ± 5.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 684.66K | ± 6.89K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 661.75K | ± 7.21K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 645.04K | ± 5.16K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56740.039    ± 149.547  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4525.525     ± 15.419  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       6404.308   ± 1253.108  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       8483.322    ± 669.286  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62851.291   ± 1149.129  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75771.525   ± 1651.470  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67259.586   ± 1184.235  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7555.797    ± 519.279  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7950.625     ± 76.554  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7618.994     ± 36.539  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        942.470     ± 16.450  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        745.577     ± 46.783  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9837.965   ± 1426.073  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4034.585    ± 145.118  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5632.146     ± 46.334  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34976.930    ± 293.096  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35429.207    ± 281.107  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     645037.651   ± 5159.976  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     661753.366   ± 7214.644  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     684662.441   ± 6885.871  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     697196.885   ± 5304.393  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
