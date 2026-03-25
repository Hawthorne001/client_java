# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-25T11:31:13Z
- **Commit:** [`6beb7fd`](https://github.com/Hawthorne001/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.52K | ± 620.69 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.94K | ± 456.70 | ops/s | 1.2x slower |
| prometheusAdd | 51.55K | ± 193.86 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.73K | ± 920.89 | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.61K | ± 9.97 | ops/s | 10x slower |
| simpleclientInc | 6.58K | ± 155.02 | ops/s | 10x slower |
| simpleclientAdd | 6.49K | ± 19.41 | ops/s | 10x slower |
| openTelemetryAdd | 1.65K | ± 258.56 | ops/s | 40x slower |
| openTelemetryInc | 1.34K | ± 210.20 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.20K | ± 43.99 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.17K | ± 974.73 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 36.64 | ops/s | 1.2x slower |
| prometheusNative | 2.66K | ± 128.59 | ops/s | 1.9x slower |
| openTelemetryClassic | 721.60 | ± 14.66 | ops/s | 7.2x slower |
| openTelemetryExponential | 562.79 | ± 22.88 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.48K | ± 2.06K | ops/s | **fastest** |
| openMetricsWriteToNull | 482.38K | ± 3.59K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 482.23K | ± 8.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.35K | ± 1.66K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48727.111    ± 920.892  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1652.454    ± 258.565  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1343.850    ± 210.199  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1200.629     ± 43.993  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51550.184    ± 193.855  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66520.458    ± 620.691  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56939.021    ± 456.703  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6490.189     ± 19.413  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6576.905    ± 155.018  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6611.827      ± 9.972  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        721.602     ± 14.655  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.792     ± 22.880  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5174.837    ± 974.734  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2661.661    ± 128.587  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4443.422     ± 36.644  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478354.844   ± 1659.111  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482375.970   ± 3589.166  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482234.056   ± 8472.197  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489482.836   ± 2063.447  ops/s
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
