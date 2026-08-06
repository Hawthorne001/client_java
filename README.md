# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-05T09:36:27Z
- **Commit:** [`922943c`](https://github.com/Hawthorne001/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 59.29K | ± 478.59 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.35K | ± 634.86 | ops/s | 1.1x slower |
| prometheusAdd | 48.49K | ± 101.31 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.82K | ± 575.80 | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 17.18K | ± 116.21 | ops/s | 3.5x slower |
| openTelemetryInc | 13.85K | ± 91.69 | ops/s | 4.3x slower |
| openTelemetryAdd | 12.06K | ± 102.81 | ops/s | 4.9x slower |
| simpleclientInc | 6.16K | ± 105.96 | ops/s | 9.6x slower |
| simpleclientAdd | 6.03K | ± 171.42 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.90K | ± 3.10 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 14.02K | ± 26.36 | ops/s | **fastest** |
| prometheusClassicSingleThread | 5.81K | ± 14.32 | ops/s | 2.4x slower |
| prometheusClassic | 4.64K | ± 588.47 | ops/s | 3.0x slower |
| simpleclient | 4.47K | ± 60.07 | ops/s | 3.1x slower |
| prometheusNative | 2.68K | ± 12.50 | ops/s | 5.2x slower |
| openTelemetryClassic | 784.19 | ± 13.04 | ops/s | 18x slower |
| openTelemetryExponential | 699.17 | ± 31.18 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.63K | ± 118.18 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.69K | ± 254.39 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 563.80K | ± 2.39K | ops/s | **fastest** |
| prometheusWriteToByteArray | 542.95K | ± 11.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 527.45K | ± 6.11K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 513.53K | ± 7.23K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44817.547    ± 575.801  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12055.054    ± 102.810  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13852.602     ± 91.690  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17179.921    ± 116.207  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48488.268    ± 101.309  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59285.798    ± 478.590  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52346.766    ± 634.859  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6032.234    ± 171.415  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6164.731    ± 105.958  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5897.857      ± 3.104  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        784.191     ± 13.039  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        699.171     ± 31.180  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4635.329    ± 588.474  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14018.829     ± 26.363  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5809.462     ± 14.319  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2675.951     ± 12.498  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4471.793     ± 60.067  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26689.791    ± 254.391  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27629.697    ± 118.183  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     513529.644   ± 7230.675  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     527454.587   ± 6111.898  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542948.184  ± 11209.664  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     563797.816   ± 2393.014  ops/s
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
