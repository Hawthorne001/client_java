# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-13T10:09:08Z
- **Commit:** [`90f99d6`](https://github.com/Hawthorne001/client_java/commit/90f99d635109472d8ccca304f044f93a1b0f1436)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.79K | ± 110.24 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.30K | ± 1.08K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.94K | ± 971.78 | ops/s | 1.3x slower |
| prometheusAdd | 48.39K | ± 3.80K | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 18.25K | ± 362.69 | ops/s | 3.6x slower |
| openTelemetryInc | 14.94K | ± 401.06 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.84K | ± 218.17 | ops/s | 5.1x slower |
| simpleclientInc | 6.53K | ± 53.50 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 32.68 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 378.34 | ops/s | 11x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.30K | ± 54.00 | ops/s | **fastest** |
| prometheusClassic | 5.05K | ± 1.08K | ops/s | 2.4x slower |
| prometheusClassicSingleThread | 4.60K | ± 49.80 | ops/s | 2.7x slower |
| simpleclient | 4.36K | ± 32.45 | ops/s | 2.8x slower |
| prometheusNative | 2.97K | ± 243.91 | ops/s | 4.1x slower |
| openTelemetryClassic | 785.86 | ± 18.53 | ops/s | 16x slower |
| openTelemetryExponential | 697.19 | ± 68.72 | ops/s | 18x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 24.07K | ± 236.35 | ops/s | **fastest** |
| prometheusWriteToNull | 23.63K | ± 738.30 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 500.02K | ± 3.18K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.06K | ± 5.19K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.80K | ± 4.32K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.65K | ± 3.01K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48937.875    ± 971.780  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12842.399    ± 218.166  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14941.792    ± 401.060  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18248.051    ± 362.686  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48389.049   ± 3804.285  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65786.382    ± 110.243  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56296.388   ± 1077.762  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6199.438    ± 378.341  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6526.006     ± 53.499  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6345.936     ± 32.677  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        785.864     ± 18.533  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        697.185     ± 68.715  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5045.698   ± 1081.680  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12304.337     ± 54.000  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4600.231     ± 49.804  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2966.336    ± 243.909  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4355.765     ± 32.452  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24066.688    ± 236.351  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23632.000    ± 738.295  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471653.455   ± 3007.632  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479803.474   ± 4317.988  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495064.937   ± 5191.458  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     500023.174   ± 3175.021  ops/s
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
