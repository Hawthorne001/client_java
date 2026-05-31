# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-31T04:52:48Z
- **Commit:** [`23f36f5`](https://github.com/Hawthorne001/client_java/commit/23f36f52b6f3792fcd5fd0c8ae2e7c306f17ef31)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.76K | ± 1.60K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.62K | ± 300.91 | ops/s | 1.2x slower |
| prometheusAdd | 51.08K | ± 771.27 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.06K | ± 262.03 | ops/s | 1.3x slower |
| simpleclientInc | 6.52K | ± 48.46 | ops/s | 10x slower |
| simpleclientAdd | 6.44K | ± 17.33 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 207.57 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.90K | ± 385.20 | ops/s | 17x slower |
| openTelemetryAdd | 3.15K | ± 393.83 | ops/s | 21x slower |
| openTelemetryInc | 3.02K | ± 153.56 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.95K | ± 108.81 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 21.64 | ops/s | 1.6x slower |
| prometheusNative | 3.10K | ± 276.52 | ops/s | 2.2x slower |
| openTelemetryClassic | 808.23 | ± 37.77 | ops/s | 8.6x slower |
| openTelemetryExponential | 575.08 | ± 3.86 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.22K | ± 813.55 | ops/s | **fastest** |
| prometheusWriteToNull | 23.27K | ± 335.01 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 504.64K | ± 2.87K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.93K | ± 3.67K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.19K | ± 3.01K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.47K | ± 4.50K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50058.468    ± 262.027  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3146.067    ± 393.833  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3017.737    ± 153.563  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3901.176    ± 385.202  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51084.621    ± 771.267  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65759.216   ± 1604.789  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56616.358    ± 300.910  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6443.688     ± 17.330  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6519.168     ± 48.461  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6389.389    ± 207.572  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        808.232     ± 37.766  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.083      ± 3.861  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6946.800    ± 108.809  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3097.578    ± 276.516  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4397.592     ± 21.639  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24224.713    ± 813.549  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23274.766    ± 335.011  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483187.562   ± 3014.416  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481465.083   ± 4495.397  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495930.873   ± 3672.732  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     504637.749   ± 2873.549  ops/s
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
