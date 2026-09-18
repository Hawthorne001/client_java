# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-17T17:56:12Z
- **Commit:** [`59ca1f0`](https://github.com/Hawthorne001/client_java/commit/59ca1f0de4637fe8f4c72baac6910b85c0e87f5d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 698.88M | ± 16468.87K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.70M | ± 486.16K | ops/s |
| prometheusLabelValuesInc | 92.85M | ± 1742.74K | ops/s |
| prometheusLabelValuesIncSingleThread | 49.92M | ± 193.35K | ops/s |
| prometheusInc | 77.56K | ± 1.28K | ops/s |
| prometheusNoLabelsInc | 66.84K | ± 1.03K | ops/s |
| prometheusAdd | 63.26K | ± 1.12K | ops/s |
| codahaleIncNoLabels | 56.34K | ± 499.97 | ops/s |
| openTelemetryIncNoLabels | 22.22K | ± 105.21 | ops/s |
| openTelemetryInc | 17.90K | ± 124.46 | ops/s |
| openTelemetryAdd | 15.75K | ± 43.98 | ops/s |
| simpleclientInc | 7.93K | ± 58.82 | ops/s |
| simpleclientAdd | 7.67K | ± 338.78 | ops/s |
| simpleclientNoLabelsInc | 7.59K | ± 15.45 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 16.84K | ± 87.44 | ops/s |
| prometheusClassic | 8.05K | ± 1.48K | ops/s |
| prometheusClassicSingleThread | 6.86K | ± 13.49 | ops/s |
| simpleclient | 5.74K | ± 190.87 | ops/s |
| prometheusNative | 3.72K | ± 248.85 | ops/s |
| openTelemetryClassic | 1.03K | ± 89.03 | ops/s |
| openTelemetryExponential | 887.36 | ± 69.05 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 35.44K | ± 291.11 | ops/s |
| openMetricsWriteToNull | 35.14K | ± 157.07 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 791.73K | ± 9.08K | ops/s |
| prometheusWriteToByteArray | 768.03K | ± 12.02K | ops/s |
| openMetricsWriteToNull | 735.98K | ± 6.64K | ops/s |
| openMetricsWriteToByteArray | 721.20K | ± 5.49K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.017 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.059 | — | — |
| CounterBenchmark.openTelemetryInc | 0.052 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.042 | — | — |
| CounterBenchmark.prometheusAdd | 0.058 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.047 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 64.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 64.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.055 | — | — |
| CounterBenchmark.simpleclientAdd | 0.122 | — | — |
| CounterBenchmark.simpleclientInc | 0.118 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.123 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.918 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.062 | — | — |
| HistogramBenchmark.prometheusClassic | 0.474 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.482 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.425 | — | — |
| HistogramBenchmark.prometheusNative | 417713.009 | — | — |
| HistogramBenchmark.simpleclient | 0.164 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.100 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.099 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56338.855    ± 499.968  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15745.242     ± 43.977  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17901.021    ± 124.455  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22216.946    ± 105.208  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63261.084   ± 1118.159  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  698875589.451 ± 16468865.033  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370696596.358 ± 486159.638  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77559.272   ± 1281.426  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15   92853915.977 ± 1742743.222  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   49915235.316 ± 193352.116  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66836.246   ± 1032.983  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7669.171    ± 338.775  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7933.007     ± 58.820  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7594.711     ± 15.450  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1027.657     ± 89.030  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        887.363     ± 69.049  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8050.096   ± 1483.993  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      16844.875     ± 87.442  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       6863.178     ± 13.490  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3717.015    ± 248.851  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5735.555    ± 190.871  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35136.017    ± 157.071  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35440.054    ± 291.111  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     721196.142   ± 5489.527  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     735981.293   ± 6637.579  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     768026.400  ± 12023.400  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     791732.138   ± 9078.243  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter updates and label-value lookup (selected methods only) |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
