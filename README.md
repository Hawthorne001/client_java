# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-15T07:21:40Z
- **Commit:** [`b81332e`](https://github.com/Hawthorne001/client_java/commit/b81332e3a09e465f956f118a2403e64b83771ae5)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.75K | ± 312.27 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.32K | ± 962.58 | ops/s | 1.2x slower |
| prometheusAdd | 51.62K | ± 135.81 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.47K | ± 1.39K | ops/s | 1.4x slower |
| simpleclientInc | 6.57K | ± 69.00 | ops/s | 10x slower |
| simpleclientAdd | 6.56K | ± 11.12 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.46K | ± 198.32 | ops/s | 10x slower |
| openTelemetryInc | 1.38K | ± 231.40 | ops/s | 48x slower |
| openTelemetryAdd | 1.33K | ± 42.33 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.26K | ± 15.83 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.66K | ± 1.01K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 35.29 | ops/s | 1.3x slower |
| prometheusNative | 2.59K | ± 59.48 | ops/s | 2.2x slower |
| openTelemetryClassic | 688.35 | ± 30.24 | ops/s | 8.2x slower |
| openTelemetryExponential | 541.59 | ± 17.73 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.50K | ± 1.96K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.15K | ± 2.35K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 489.35K | ± 5.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.22K | ± 3.39K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48474.611   ± 1391.671  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1328.613     ± 42.335  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1382.338    ± 231.401  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1260.666     ± 15.825  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51624.288    ± 135.812  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65745.150    ± 312.268  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56323.969    ± 962.579  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6563.549     ± 11.122  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6574.246     ± 68.999  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6459.314    ± 198.321  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        688.353     ± 30.241  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.590     ± 17.725  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5659.607   ± 1013.757  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2589.389     ± 59.478  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4507.869     ± 35.287  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     489352.223   ± 5793.542  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489215.907   ± 3388.670  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495145.369   ± 2345.647  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495498.122   ± 1960.271  ops/s
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
