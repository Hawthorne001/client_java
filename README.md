# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-27T19:28:52Z
- **Commit:** [`28e49da`](https://github.com/Hawthorne001/client_java/commit/28e49dac7fd80d6c83adfb054a23e9e15ce627b6)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.04K | ± 532.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.03K | ± 417.11 | ops/s | 1.2x slower |
| prometheusAdd | 51.37K | ± 238.41 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.57K | ± 1.19K | ops/s | 1.4x slower |
| simpleclientInc | 6.74K | ± 19.03 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.51K | ± 170.44 | ops/s | 10x slower |
| simpleclientAdd | 6.45K | ± 166.79 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 232.53 | ops/s | 46x slower |
| openTelemetryInc | 1.25K | ± 34.45 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.19K | ± 18.95 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.56K | ± 45.44 | ops/s | **fastest** |
| prometheusClassic | 4.46K | ± 705.63 | ops/s | 1.0x slower |
| prometheusNative | 2.60K | ± 124.31 | ops/s | 1.8x slower |
| openTelemetryClassic | 661.23 | ± 19.95 | ops/s | 6.9x slower |
| openTelemetryExponential | 538.57 | ± 3.09 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.06K | ± 2.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.31K | ± 4.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.17K | ± 4.16K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.55K | ± 4.09K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48570.771   ± 1190.457  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1432.116    ± 232.525  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1247.204     ± 34.449  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1187.816     ± 18.945  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51374.054    ± 238.411  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66039.189    ± 532.034  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57032.506    ± 417.107  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6446.828    ± 166.792  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6744.067     ± 19.030  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6507.208    ± 170.435  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        661.226     ± 19.949  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        538.567      ± 3.089  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4463.179    ± 705.628  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2598.166    ± 124.305  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4556.389     ± 45.441  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474549.708   ± 4091.280  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477172.126   ± 4163.021  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485306.084   ± 4697.564  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491056.414   ± 2167.733  ops/s
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
