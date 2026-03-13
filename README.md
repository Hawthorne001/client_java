# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-13T06:31:07Z
- **Commit:** [`e854af4`](https://github.com/Hawthorne001/client_java/commit/e854af48392c5ad5535a153bafa62253d2dced24)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.49K | ± 2.44K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.21K | ± 87.39 | ops/s | 1.1x slower |
| prometheusAdd | 51.32K | ± 669.14 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.40K | ± 1.17K | ops/s | 1.3x slower |
| simpleclientInc | 6.75K | ± 42.40 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.71K | ± 7.76 | ops/s | 9.6x slower |
| simpleclientAdd | 6.53K | ± 39.47 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.56K | ± 356.93 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.34K | ± 157.82 | ops/s | 48x slower |
| openTelemetryInc | 1.31K | ± 116.10 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 463.35 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 16.76 | ops/s | 1.2x slower |
| prometheusNative | 2.84K | ± 264.12 | ops/s | 1.9x slower |
| openTelemetryClassic | 703.92 | ± 14.14 | ops/s | 7.8x slower |
| openTelemetryExponential | 584.66 | ± 46.21 | ops/s | 9.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 489.35K | ± 2.64K | ops/s | **fastest** |
| prometheusWriteToNull | 489.28K | ± 6.05K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.91K | ± 6.65K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.38K | ± 9.34K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48401.795   ± 1170.669  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1562.245    ± 356.928  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1314.026    ± 116.104  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1344.100    ± 157.820  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51316.021    ± 669.145  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64489.005   ± 2438.373  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57206.689     ± 87.390  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6532.991     ± 39.473  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6752.556     ± 42.400  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6709.150      ± 7.763  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        703.920     ± 14.140  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        584.657     ± 46.210  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5502.576    ± 463.353  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2839.969    ± 264.118  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4544.316     ± 16.761  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481381.924   ± 9336.636  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485907.893   ± 6645.711  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489348.103   ± 2640.449  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489277.184   ± 6054.061  ops/s
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
