# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-01T20:43:24Z
- **Commit:** [`6938479`](https://github.com/Hawthorne001/client_java/commit/69384791685f0e86a28f04191434ecab310365ba)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.73K | ± 521.70 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.31K | ± 1.04K | ops/s | 1.2x slower |
| prometheusAdd | 51.37K | ± 469.52 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.71K | ± 2.24K | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 114.41 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.42K | ± 209.58 | ops/s | 10x slower |
| simpleclientAdd | 6.41K | ± 198.88 | ops/s | 10x slower |
| openTelemetryAdd | 1.41K | ± 210.04 | ops/s | 47x slower |
| openTelemetryInc | 1.25K | ± 38.68 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.18K | ± 38.43 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.98K | ± 484.87 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 15.21 | ops/s | 1.1x slower |
| prometheusNative | 2.84K | ± 289.00 | ops/s | 1.8x slower |
| openTelemetryClassic | 674.63 | ± 27.27 | ops/s | 7.4x slower |
| openTelemetryExponential | 575.18 | ± 24.98 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.93K | ± 3.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.44K | ± 2.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.86K | ± 5.56K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.57K | ± 4.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47706.675   ± 2236.083  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1413.894    ± 210.045  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1247.403     ± 38.678  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1175.255     ± 38.428  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51367.121    ± 469.522  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66730.276    ± 521.703  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56305.447   ± 1035.308  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6414.435    ± 198.881  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6684.442    ± 114.411  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6424.315    ± 209.585  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        674.628     ± 27.271  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.182     ± 24.977  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4978.685    ± 484.867  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2844.670    ± 289.000  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4556.081     ± 15.212  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481568.897   ± 4718.706  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485856.054   ± 5561.415  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490440.531   ± 2040.978  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493929.050   ± 3347.707  ops/s
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
