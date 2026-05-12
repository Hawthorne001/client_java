# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-12T15:01:00Z
- **Commit:** [`11cb921`](https://github.com/Hawthorne001/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.31K | ± 1.57K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.73K | ± 539.84 | ops/s | 1.1x slower |
| prometheusAdd | 61.52K | ± 424.10 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.69K | ± 144.20 | ops/s | 1.3x slower |
| simpleclientInc | 7.97K | ± 68.30 | ops/s | 9.6x slower |
| simpleclientAdd | 7.86K | ± 8.27 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 7.61K | ± 8.75 | ops/s | 10x slower |
| openTelemetryInc | 6.81K | ± 1.16K | ops/s | 11x slower |
| openTelemetryIncNoLabels | 4.97K | ± 538.19 | ops/s | 15x slower |
| openTelemetryAdd | 4.84K | ± 1.18K | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.63K | ± 1.96K | ops/s | **fastest** |
| simpleclient | 5.37K | ± 127.61 | ops/s | 1.2x slower |
| prometheusNative | 3.82K | ± 356.76 | ops/s | 1.7x slower |
| openTelemetryClassic | 891.77 | ± 21.87 | ops/s | 7.4x slower |
| openTelemetryExponential | 716.75 | ± 14.36 | ops/s | 9.2x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 35.35K | ± 587.49 | ops/s | **fastest** |
| openMetricsWriteToNull | 34.69K | ± 129.75 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 705.49K | ± 2.08K | ops/s | **fastest** |
| prometheusWriteToByteArray | 685.94K | ± 7.09K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 660.08K | ± 4.61K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 645.69K | ± 4.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56689.901    ± 144.203  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4844.238   ± 1183.011  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       6805.093   ± 1164.753  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4973.559    ± 538.191  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61520.842    ± 424.097  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76308.107   ± 1570.682  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67731.474    ± 539.835  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7855.393      ± 8.267  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7966.558     ± 68.301  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7605.597      ± 8.754  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        891.770     ± 21.867  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        716.754     ± 14.356  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6625.848   ± 1957.008  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3815.661    ± 356.755  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5371.239    ± 127.611  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34689.362    ± 129.746  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35354.657    ± 587.492  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     645689.452   ± 4058.732  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     660080.730   ± 4609.491  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     685938.050   ± 7086.222  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     705493.187   ± 2076.703  ops/s
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
