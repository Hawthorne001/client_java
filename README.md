# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-22T21:35:07Z
- **Commit:** [`320538a`](https://github.com/Hawthorne001/client_java/commit/320538a09efad128c6d80bcc3d6eecca394603db)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.01K | ± 1.33K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.39K | ± 868.46 | ops/s | 1.2x slower |
| prometheusAdd | 51.49K | ± 135.85 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.03K | ± 1.69K | ops/s | 1.4x slower |
| simpleclientInc | 6.52K | ± 10.06 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.27K | ± 41.55 | ops/s | 10x slower |
| simpleclientAdd | 6.15K | ± 221.19 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.74K | ± 300.85 | ops/s | 17x slower |
| openTelemetryInc | 3.34K | ± 644.93 | ops/s | 19x slower |
| openTelemetryAdd | 3.26K | ± 273.17 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.93K | ± 962.52 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 89.73 | ops/s | 1.6x slower |
| prometheusNative | 2.76K | ± 289.11 | ops/s | 2.5x slower |
| openTelemetryClassic | 759.54 | ± 17.87 | ops/s | 9.1x slower |
| openTelemetryExponential | 659.20 | ± 56.87 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.89K | ± 154.61 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.87K | ± 414.74 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 503.84K | ± 7.52K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.54K | ± 7.52K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.66K | ± 3.93K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 462.03K | ± 6.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48030.202   ± 1690.537  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3260.788    ± 273.171  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3340.707    ± 644.929  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3741.885    ± 300.851  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51487.813    ± 135.847  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65010.979   ± 1330.485  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56389.401    ± 868.462  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6154.512    ± 221.194  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6523.239     ± 10.060  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6270.424     ± 41.555  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        759.536     ± 17.869  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        659.198     ± 56.866  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6932.466    ± 962.522  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2755.699    ± 289.110  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4405.422     ± 89.732  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23871.419    ± 414.739  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23890.772    ± 154.610  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     462026.320   ± 6466.468  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481662.192   ± 3932.603  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491535.271   ± 7522.643  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     503842.106   ± 7520.567  ops/s
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
