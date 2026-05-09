# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-09T13:57:25Z
- **Commit:** [`317347c`](https://github.com/Hawthorne001/client_java/commit/317347c6ab5ee6f2ed5c963bb71f39b2a1d624be)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.86K | ± 755.63 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 318.05 | ops/s | 1.2x slower |
| prometheusAdd | 51.35K | ± 208.14 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 42.89K | ± 7.04K | ops/s | 1.6x slower |
| simpleclientInc | 6.63K | ± 73.09 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 15.63 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.31K | ± 49.04 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.39K | ± 247.79 | ops/s | 20x slower |
| openTelemetryAdd | 3.25K | ± 149.57 | ops/s | 21x slower |
| openTelemetryInc | 3.14K | ± 143.50 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.71K | ± 1.13K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 96.95 | ops/s | 1.3x slower |
| prometheusNative | 3.08K | ± 199.04 | ops/s | 1.9x slower |
| openTelemetryClassic | 793.35 | ± 22.53 | ops/s | 7.2x slower |
| openTelemetryExponential | 628.14 | ± 57.54 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.32K | ± 145.92 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.94K | ± 159.35 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 512.18K | ± 5.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.37K | ± 3.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.02K | ± 1.79K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 475.46K | ± 6.37K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42894.856   ± 7035.104  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3248.461    ± 149.570  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3141.323    ± 143.501  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3385.151    ± 247.793  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51352.661    ± 208.144  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66859.607    ± 755.627  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56926.354    ± 318.055  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6457.642     ± 15.632  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6625.540     ± 73.093  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6314.894     ± 49.040  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        793.345     ± 22.532  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        628.141     ± 57.539  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5711.826   ± 1134.431  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3078.324    ± 199.035  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.281     ± 96.954  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23939.018    ± 159.353  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24315.122    ± 145.922  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475460.382   ± 6372.978  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486018.838   ± 1792.837  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503365.801   ± 3220.043  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512184.696   ± 5120.501  ops/s
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
