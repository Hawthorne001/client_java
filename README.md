# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-01T09:36:54Z
- **Commit:** [`3404554`](https://github.com/Hawthorne001/client_java/commit/34045542970750463b2956e426388fdaca0d3b07)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 59.13K | ± 174.73 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.57K | ± 472.38 | ops/s | 1.1x slower |
| prometheusAdd | 48.45K | ± 951.00 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.05K | ± 1.09K | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 16.87K | ± 209.13 | ops/s | 3.5x slower |
| openTelemetryInc | 13.74K | ± 194.48 | ops/s | 4.3x slower |
| openTelemetryAdd | 12.09K | ± 131.54 | ops/s | 4.9x slower |
| simpleclientInc | 6.16K | ± 63.25 | ops/s | 9.6x slower |
| simpleclientAdd | 6.14K | ± 57.10 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.02K | ± 163.38 | ops/s | 9.8x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 14.49K | ± 184.78 | ops/s | **fastest** |
| prometheusClassicSingleThread | 5.94K | ± 4.05 | ops/s | 2.4x slower |
| prometheusClassic | 5.86K | ± 2.70K | ops/s | 2.5x slower |
| simpleclient | 4.54K | ± 40.01 | ops/s | 3.2x slower |
| prometheusNative | 2.90K | ± 249.24 | ops/s | 5.0x slower |
| openTelemetryClassic | 779.77 | ± 44.23 | ops/s | 19x slower |
| openTelemetryExponential | 671.15 | ± 47.08 | ops/s | 22x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.71K | ± 167.16 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.15K | ± 282.29 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 580.15K | ± 10.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 571.10K | ± 1.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 547.93K | ± 2.22K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 535.78K | ± 3.02K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43051.937   ± 1090.836  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12090.071    ± 131.540  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13738.254    ± 194.481  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      16869.662    ± 209.128  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48452.197    ± 950.998  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59125.555    ± 174.730  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51568.841    ± 472.379  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6138.318     ± 57.096  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6163.559     ± 63.248  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6024.001    ± 163.382  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        779.774     ± 44.234  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        671.155     ± 47.077  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5855.639   ± 2702.183  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14491.009    ± 184.779  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5942.784      ± 4.045  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2904.952    ± 249.235  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4542.350     ± 40.007  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27149.334    ± 282.293  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27707.557    ± 167.156  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     535777.553   ± 3021.516  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     547932.541   ± 2219.247  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     571096.187   ± 1274.448  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     580147.424  ± 10270.243  ops/s
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
