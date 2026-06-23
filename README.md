# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-22T08:13:14Z
- **Commit:** [`da14412`](https://github.com/Hawthorne001/client_java/commit/da144125367c0410df66120631f6cae5ead25fcb)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.16K | ± 1.05K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.12K | ± 536.34 | ops/s | 1.2x slower |
| prometheusAdd | 48.23K | ± 242.79 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.46K | ± 738.12 | ops/s | 1.4x slower |
| simpleclientInc | 6.17K | ± 55.26 | ops/s | 9.8x slower |
| simpleclientAdd | 5.95K | ± 175.15 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.87K | ± 43.23 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.47K | ± 929.83 | ops/s | 11x slower |
| openTelemetryAdd | 5.21K | ± 73.00 | ops/s | 12x slower |
| openTelemetryInc | 4.27K | ± 148.43 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.45K | ± 1.16K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 154.76 | ops/s | 1.2x slower |
| prometheusNative | 2.89K | ± 236.82 | ops/s | 1.9x slower |
| openTelemetryClassic | 777.01 | ± 25.38 | ops/s | 7.0x slower |
| openTelemetryExponential | 569.23 | ± 18.96 | ops/s | 9.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.38K | ± 131.87 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.26K | ± 239.44 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 582.77K | ± 5.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 572.89K | ± 3.09K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 548.26K | ± 5.44K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 533.97K | ± 4.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44455.123    ± 738.117  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5210.055     ± 73.000  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4265.913    ± 148.426  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5470.755    ± 929.827  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48232.255    ± 242.791  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60157.186   ± 1046.323  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51121.253    ± 536.337  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5947.442    ± 175.149  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6165.359     ± 55.261  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5874.593     ± 43.228  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        777.015     ± 25.381  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.230     ± 18.956  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5451.745   ± 1156.628  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2888.088    ± 236.817  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4506.288    ± 154.760  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27259.276    ± 239.441  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27384.497    ± 131.865  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     533966.224   ± 4198.760  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     548261.483   ± 5436.660  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     572887.540   ± 3089.626  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     582774.517   ± 4995.039  ops/s
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
