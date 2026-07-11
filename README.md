# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-10T11:27:06Z
- **Commit:** [`79a5990`](https://github.com/Hawthorne001/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.96K | ± 1.88K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.01K | ± 411.31 | ops/s | 1.1x slower |
| prometheusAdd | 51.14K | ± 166.28 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.07K | ± 1.49K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 38.65 | ops/s | 9.9x slower |
| simpleclientAdd | 6.41K | ± 53.71 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 6.48 | ops/s | 10x slower |
| openTelemetryInc | 3.52K | ± 235.38 | ops/s | 18x slower |
| openTelemetryAdd | 3.28K | ± 370.79 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.15K | ± 335.66 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.57K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 4.34K | ± 14.23 | ops/s | 1.3x slower |
| prometheusNative | 3.15K | ± 145.78 | ops/s | 1.8x slower |
| openTelemetryClassic | 729.49 | ± 36.79 | ops/s | 7.6x slower |
| openTelemetryExponential | 705.56 | ± 34.17 | ops/s | 7.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.68K | ± 111.79 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.62K | ± 692.32 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 508.25K | ± 10.29K | ops/s | **fastest** |
| prometheusWriteToByteArray | 501.58K | ± 3.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 493.53K | ± 1.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 487.94K | ± 2.56K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49069.946   ± 1492.399  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3282.098    ± 370.787  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3515.367    ± 235.380  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3145.154    ± 335.662  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51138.862    ± 166.282  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64961.821   ± 1876.272  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57007.538    ± 411.311  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6413.499     ± 53.706  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6531.581     ± 38.649  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6336.733      ± 6.480  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        729.487     ± 36.788  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        705.562     ± 34.168  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5567.785   ± 1435.019  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3148.897    ± 145.782  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4343.648     ± 14.226  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23624.009    ± 692.321  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23677.300    ± 111.789  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     487942.881   ± 2560.767  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     493532.712   ± 1446.935  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     501575.421   ± 3220.456  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508254.863  ± 10288.035  ops/s
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
