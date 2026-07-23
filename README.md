# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-22T10:11:22Z
- **Commit:** [`0a91771`](https://github.com/Hawthorne001/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 64.23K | ± 1.40K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.73K | ± 394.01 | ops/s | 1.1x slower |
| prometheusAdd | 51.17K | ± 310.37 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.02K | ± 448.73 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 10.35 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.35K | ± 7.81 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 192.58 | ops/s | 10x slower |
| openTelemetryInc | 3.36K | ± 452.69 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.16K | ± 252.79 | ops/s | 20x slower |
| openTelemetryAdd | 3.08K | ± 189.60 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.45K | ± 127.32 | ops/s | **fastest** |
| prometheusClassic | 5.52K | ± 1.32K | ops/s | 2.3x slower |
| prometheusClassicSingleThread | 4.38K | ± 374.11 | ops/s | 2.8x slower |
| simpleclient | 4.37K | ± 44.16 | ops/s | 2.8x slower |
| prometheusNative | 2.91K | ± 311.50 | ops/s | 4.3x slower |
| openTelemetryClassic | 794.23 | ± 11.51 | ops/s | 16x slower |
| openTelemetryExponential | 579.34 | ± 5.25 | ops/s | 21x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 23.80K | ± 386.07 | ops/s | **fastest** |
| prometheusWriteToNull | 23.55K | ± 397.94 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 512.04K | ± 11.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.98K | ± 4.03K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.55K | ± 2.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 488.11K | ± 5.24K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50015.149    ± 448.732  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3076.917    ± 189.596  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3364.871    ± 452.687  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3159.245    ± 252.789  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51171.053    ± 310.365  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64226.515   ± 1395.010  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56728.660    ± 394.012  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6343.989    ± 192.575  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6578.121     ± 10.346  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6348.067      ± 7.808  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        794.234     ± 11.513  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        579.340      ± 5.249  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5521.146   ± 1318.058  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12452.320    ± 127.322  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4384.474    ± 374.112  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2909.478    ± 311.496  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4374.222     ± 44.157  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23802.439    ± 386.065  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23550.981    ± 397.936  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488113.515   ± 5235.129  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489548.003   ± 2273.259  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503975.965   ± 4025.843  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512037.944  ± 11205.744  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
