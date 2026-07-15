# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-14T11:13:09Z
- **Commit:** [`63967bd`](https://github.com/Hawthorne001/client_java/commit/63967bd36ebc638234742ec58ad28f6098a92b3a)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 60.20K | ± 1.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.90K | ± 57.42 | ops/s | 1.2x slower |
| prometheusAdd | 48.05K | ± 520.03 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.54K | ± 1.46K | ops/s | 1.4x slower |
| simpleclientInc | 6.19K | ± 87.18 | ops/s | 9.7x slower |
| simpleclientAdd | 6.10K | ± 25.26 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.90K | ± 42.38 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.66K | ± 1.47K | ops/s | 13x slower |
| openTelemetryInc | 4.61K | ± 1.28K | ops/s | 13x slower |
| openTelemetryAdd | 4.43K | ± 815.55 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassic | 4.48K | ± 512.98 | ops/s | **fastest** |
| simpleclient | 3.90K | ± 50.31 | ops/s | 1.1x slower |
| prometheusNative | 2.60K | ± 231.66 | ops/s | 1.7x slower |
| openTelemetryClassic | 740.62 | ± 8.88 | ops/s | 6.1x slower |
| openTelemetryExponential | 587.31 | ± 32.26 | ops/s | 7.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.81K | ± 198.20 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.48K | ± 166.44 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 581.68K | ± 9.07K | ops/s | **fastest** |
| prometheusWriteToByteArray | 568.60K | ± 4.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 550.78K | ± 3.75K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 483.27K | ± 8.63K | ops/s | 1.2x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43541.783   ± 1462.948  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4433.990    ± 815.554  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4613.917   ± 1281.388  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4659.486   ± 1473.721  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48047.376    ± 520.029  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60198.283   ± 1152.524  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50903.014     ± 57.416  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6096.306     ± 25.264  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6190.983     ± 87.176  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5895.788     ± 42.377  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        740.624      ± 8.883  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        587.307     ± 32.256  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4481.954    ± 512.980  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2603.232    ± 231.657  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       3904.185     ± 50.309  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23484.072    ± 166.444  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23813.694    ± 198.197  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483269.150   ± 8629.888  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     550778.485   ± 3752.202  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     568603.514   ± 4871.117  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581677.882   ± 9071.058  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
