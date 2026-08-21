# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-20T11:39:22Z
- **Commit:** [`c8e2c03`](https://github.com/Hawthorne001/client_java/commit/c8e2c03788424cac089ff2772463f00fa6f33afa)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 60.03K | ± 1.02K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.91K | ± 36.35 | ops/s | 1.2x slower |
| prometheusAdd | 49.16K | ± 912.32 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.07K | ± 146.92 | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 17.08K | ± 255.74 | ops/s | 3.5x slower |
| openTelemetryInc | 13.54K | ± 327.78 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.12K | ± 93.56 | ops/s | 5.0x slower |
| simpleclientInc | 6.16K | ± 57.56 | ops/s | 9.7x slower |
| simpleclientAdd | 6.00K | ± 183.81 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.00K | ± 189.13 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 13.77K | ± 107.68 | ops/s | **fastest** |
| prometheusClassic | 6.20K | ± 1.84K | ops/s | 2.2x slower |
| prometheusClassicSingleThread | 5.80K | ± 23.04 | ops/s | 2.4x slower |
| simpleclient | 4.62K | ± 47.55 | ops/s | 3.0x slower |
| prometheusNative | 3.02K | ± 112.80 | ops/s | 4.6x slower |
| openTelemetryClassic | 810.52 | ± 42.95 | ops/s | 17x slower |
| openTelemetryExponential | 738.76 | ± 46.45 | ops/s | 19x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.57K | ± 187.83 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.27K | ± 290.22 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 565.28K | ± 3.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 557.03K | ± 4.61K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.16K | ± 5.58K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 518.99K | ± 3.89K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44070.330    ± 146.923  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12121.007     ± 93.563  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13540.790    ± 327.777  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17084.714    ± 255.738  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49157.548    ± 912.317  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60033.182   ± 1015.156  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50907.221     ± 36.349  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6004.637    ± 183.808  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6158.939     ± 57.562  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5996.985    ± 189.127  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        810.518     ± 42.955  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        738.755     ± 46.452  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6199.992   ± 1843.717  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13766.378    ± 107.682  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5802.908     ± 23.041  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3016.729    ± 112.798  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4615.048     ± 47.549  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27274.081    ± 290.217  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27569.294    ± 187.827  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     518991.886   ± 3890.732  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534160.076   ± 5578.046  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     557030.545   ± 4610.351  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     565282.025   ± 3189.062  ops/s
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
