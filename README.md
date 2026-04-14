# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-14T21:40:22Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.94K | ± 1.95K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.25K | ± 145.66 | ops/s | 1.1x slower |
| prometheusAdd | 51.35K | ± 221.28 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.14K | ± 1.06K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 189.24 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.52K | ± 149.49 | ops/s | 10.0x slower |
| simpleclientAdd | 6.29K | ± 280.34 | ops/s | 10x slower |
| openTelemetryInc | 1.52K | ± 210.61 | ops/s | 43x slower |
| openTelemetryAdd | 1.23K | ± 43.31 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.19K | ± 48.88 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.79K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 81.14 | ops/s | 1.3x slower |
| prometheusNative | 3.00K | ± 378.22 | ops/s | 1.9x slower |
| openTelemetryClassic | 675.51 | ± 12.82 | ops/s | 8.6x slower |
| openTelemetryExponential | 566.66 | ± 8.63 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.64K | ± 3.64K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.12K | ± 3.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.74K | ± 7.82K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.04K | ± 4.62K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49137.093   ± 1055.574  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1230.688     ± 43.313  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1522.975    ± 210.608  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1189.412     ± 48.882  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51353.072    ± 221.280  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64939.207   ± 1945.549  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57250.229    ± 145.660  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6287.517    ± 280.336  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6529.140    ± 189.243  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6515.859    ± 149.494  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        675.511     ± 12.824  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.662      ± 8.626  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5793.185   ± 1309.123  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3002.872    ± 378.223  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4467.008     ± 81.143  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463044.849   ± 4622.279  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474735.075   ± 7817.422  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481124.875   ± 3169.281  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486636.622   ± 3639.810  ops/s
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
