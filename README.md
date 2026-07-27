# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-26T09:56:11Z
- **Commit:** [`7c081da`](https://github.com/Hawthorne001/client_java/commit/7c081da30c522abb0b931d3800bbc5f3b2904ad4)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 78.53K | ± 1.00K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.05K | ± 451.14 | ops/s | 1.2x slower |
| prometheusAdd | 62.88K | ± 1.19K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 55.28K | ± 2.20K | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 22.08K | ± 72.11 | ops/s | 3.6x slower |
| openTelemetryInc | 17.71K | ± 249.61 | ops/s | 4.4x slower |
| openTelemetryAdd | 15.34K | ± 519.87 | ops/s | 5.1x slower |
| simpleclientInc | 7.86K | ± 83.77 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 7.75K | ± 231.94 | ops/s | 10x slower |
| simpleclientAdd | 7.72K | ± 167.52 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 18.82K | ± 87.74 | ops/s | **fastest** |
| prometheusClassic | 8.27K | ± 1.82K | ops/s | 2.3x slower |
| prometheusClassicSingleThread | 7.64K | ± 26.74 | ops/s | 2.5x slower |
| simpleclient | 5.82K | ± 62.15 | ops/s | 3.2x slower |
| prometheusNative | 3.87K | ± 379.98 | ops/s | 4.9x slower |
| openTelemetryClassic | 954.45 | ± 31.19 | ops/s | 20x slower |
| openTelemetryExponential | 841.93 | ± 66.59 | ops/s | 22x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 35.54K | ± 484.59 | ops/s | **fastest** |
| openMetricsWriteToNull | 35.02K | ± 317.43 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 702.35K | ± 4.70K | ops/s | **fastest** |
| prometheusWriteToByteArray | 691.67K | ± 6.93K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 662.75K | ± 5.79K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 644.82K | ± 1.60K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55275.761   ± 2204.221  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15340.497    ± 519.865  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17713.535    ± 249.605  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22079.159     ± 72.114  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62884.449   ± 1193.180  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      78527.972   ± 1003.154  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66045.163    ± 451.139  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7723.886    ± 167.516  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7860.147     ± 83.766  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7754.794    ± 231.942  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        954.446     ± 31.187  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        841.926     ± 66.586  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8269.630   ± 1824.797  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      18824.922     ± 87.744  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7638.448     ± 26.737  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3871.990    ± 379.976  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5815.370     ± 62.153  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35021.158    ± 317.435  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35544.017    ± 484.590  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     644820.214   ± 1601.058  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     662747.667   ± 5786.482  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     691671.577   ± 6932.803  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     702351.334   ± 4697.099  ops/s
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
