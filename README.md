# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-10T13:28:25Z
- **Commit:** [`11cb921`](https://github.com/Hawthorne001/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.78K | ± 97.09 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.85K | ± 962.92 | ops/s | 1.2x slower |
| prometheusAdd | 51.05K | ± 681.32 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.89K | ± 1.32K | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 42.81 | ops/s | 10x slower |
| simpleclientAdd | 6.49K | ± 49.29 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 36.92 | ops/s | 10x slower |
| openTelemetryAdd | 3.26K | ± 55.26 | ops/s | 20x slower |
| openTelemetryInc | 3.07K | ± 383.52 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 2.99K | ± 232.31 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.61K | ± 1.18K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 46.64 | ops/s | 1.3x slower |
| prometheusNative | 2.72K | ± 283.73 | ops/s | 2.1x slower |
| openTelemetryClassic | 757.03 | ± 39.30 | ops/s | 7.4x slower |
| openTelemetryExponential | 722.37 | ± 122.85 | ops/s | 7.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.22K | ± 434.00 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.42K | ± 774.78 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 505.03K | ± 2.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 497.16K | ± 3.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.93K | ± 2.19K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 474.07K | ± 3.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48888.361   ± 1324.707  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3255.180     ± 55.257  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3065.110    ± 383.519  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2987.953    ± 232.311  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51046.725    ± 681.315  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65777.193     ± 97.094  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55846.448    ± 962.920  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6489.972     ± 49.286  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6567.529     ± 42.811  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6358.917     ± 36.917  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        757.027     ± 39.295  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        722.369    ± 122.854  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5607.942   ± 1178.153  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2717.580    ± 283.734  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4421.093     ± 46.636  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23418.453    ± 774.781  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24219.920    ± 434.005  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474068.537   ± 3484.067  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479932.180   ± 2185.437  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     497159.894   ± 3904.199  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     505033.914   ± 2274.496  ops/s
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
