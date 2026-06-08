# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-07T05:39:31Z
- **Commit:** [`de73848`](https://github.com/Hawthorne001/client_java/commit/de738487b85e8f85d8d3d79c54b8d05b739a7e42)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.57K | ± 500.53 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.53K | ± 906.96 | ops/s | 1.2x slower |
| prometheusAdd | 47.79K | ± 87.30 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.46K | ± 1.48K | ops/s | 1.4x slower |
| simpleclientInc | 6.16K | ± 46.58 | ops/s | 9.7x slower |
| simpleclientAdd | 6.03K | ± 165.86 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.91K | ± 27.21 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.77K | ± 1.17K | ops/s | 12x slower |
| openTelemetryInc | 3.83K | ± 284.94 | ops/s | 16x slower |
| openTelemetryAdd | 3.73K | ± 951.82 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.54K | ± 38.16 | ops/s | **fastest** |
| prometheusClassic | 4.43K | ± 727.31 | ops/s | 1.0x slower |
| prometheusNative | 2.73K | ± 189.19 | ops/s | 1.7x slower |
| openTelemetryClassic | 718.42 | ± 46.58 | ops/s | 6.3x slower |
| openTelemetryExponential | 529.39 | ± 14.49 | ops/s | 8.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.36K | ± 254.52 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.35K | ± 262.51 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 579.87K | ± 13.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 572.41K | ± 4.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 543.89K | ± 5.16K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 532.40K | ± 8.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43463.194   ± 1475.294  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3729.431    ± 951.818  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3827.740    ± 284.945  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4771.524   ± 1173.644  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47792.400     ± 87.305  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59567.673    ± 500.526  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51530.990    ± 906.955  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6028.918    ± 165.863  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6156.863     ± 46.580  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5913.330     ± 27.211  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        718.421     ± 46.585  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        529.388     ± 14.487  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4431.525    ± 727.311  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2731.108    ± 189.189  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4544.751     ± 38.162  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27351.252    ± 262.507  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27356.280    ± 254.516  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     532397.559   ± 8323.222  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     543892.199   ± 5162.997  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     572408.345   ± 4498.354  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     579869.772  ± 13149.901  ops/s
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
