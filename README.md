# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-24T09:03:46Z
- **Commit:** [`a017f80`](https://github.com/Hawthorne001/client_java/commit/a017f80980d91a5fa8ffe930c820f836c3d1b2ff)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.90K | ± 433.55 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.07K | ± 1.09K | ops/s | 1.2x slower |
| prometheusAdd | 50.98K | ± 619.10 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.29K | ± 573.86 | ops/s | 1.4x slower |
| simpleclientInc | 6.55K | ± 41.11 | ops/s | 10x slower |
| simpleclientAdd | 6.48K | ± 67.48 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.33K | ± 27.37 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.25K | ± 296.87 | ops/s | 20x slower |
| openTelemetryInc | 3.11K | ± 52.73 | ops/s | 21x slower |
| openTelemetryAdd | 3.04K | ± 57.70 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.70K | ± 465.14 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 47.85 | ops/s | 1.5x slower |
| prometheusNative | 2.98K | ± 303.82 | ops/s | 2.3x slower |
| openTelemetryClassic | 789.98 | ± 25.06 | ops/s | 8.5x slower |
| openTelemetryExponential | 594.47 | ± 55.08 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.99K | ± 486.16 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.19K | ± 408.16 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 456.09K | ± 4.62K | ops/s | **fastest** |
| prometheusWriteToNull | 454.98K | ± 7.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 437.30K | ± 4.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 426.65K | ± 5.22K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46289.278    ± 573.862  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3038.514     ± 57.701  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3113.158     ± 52.733  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3251.747    ± 296.870  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50983.427    ± 619.096  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65903.560    ± 433.545  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56066.959   ± 1094.271  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6484.388     ± 67.483  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6551.558     ± 41.106  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6328.610     ± 27.372  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        789.985     ± 25.059  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        594.467     ± 55.078  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6702.712    ± 465.139  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2975.727    ± 303.824  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4421.349     ± 47.847  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23185.158    ± 408.160  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23993.686    ± 486.161  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     426650.121   ± 5222.293  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     437299.721   ± 4521.342  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     456090.889   ± 4619.495  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     454978.161   ± 7119.302  ops/s
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
