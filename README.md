# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-21T17:49:28Z
- **Commit:** [`0d800d0`](https://github.com/Hawthorne001/client_java/commit/0d800d0a91578e48f34909472c183174fdf1d83e)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.75K | ± 2.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.09K | ± 860.48 | ops/s | 1.2x slower |
| prometheusAdd | 51.15K | ± 862.05 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.81K | ± 1.91K | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 43.25 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.70K | ± 6.43 | ops/s | 9.7x slower |
| simpleclientAdd | 6.26K | ± 250.59 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 206.00 | ops/s | 45x slower |
| openTelemetryInc | 1.21K | ± 23.26 | ops/s | 54x slower |
| openTelemetryIncNoLabels | 1.20K | ± 32.82 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.88K | ± 1.36K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 59.79 | ops/s | 1.3x slower |
| prometheusNative | 2.82K | ± 383.20 | ops/s | 2.1x slower |
| openTelemetryClassic | 704.75 | ± 46.99 | ops/s | 8.3x slower |
| openTelemetryExponential | 525.87 | ± 25.58 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.28K | ± 2.02K | ops/s | **fastest** |
| prometheusWriteToByteArray | 483.31K | ± 6.35K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.22K | ± 4.28K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.94K | ± 3.57K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48814.567   ± 1907.324  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1431.327    ± 205.999  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1207.882     ± 23.262  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1196.596     ± 32.820  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51147.769    ± 862.045  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64751.580   ± 2044.130  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56090.312    ± 860.481  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6258.015    ± 250.593  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6713.438     ± 43.247  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6699.455      ± 6.426  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.748     ± 46.990  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        525.869     ± 25.579  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5880.516   ± 1364.965  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2816.762    ± 383.205  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4512.760     ± 59.785  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473938.284   ± 3568.471  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481221.083   ± 4276.138  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483312.122   ± 6350.029  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492279.229   ± 2020.817  ops/s
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
