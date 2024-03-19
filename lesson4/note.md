# Lesson 4

## Agenda

Use hadoop to run below example:

- Wordcount
- Pi
- Secondary Sort

## Steps

### 1. login to the hadoop master namenode

```bash
docker exec -it lesson4_namenode_1 bash
```

### 2. Install curl wget and vim

```bash
sudo apt update && sudo apt install -y curl wget vim
```

### 3. Get wordcount example data

```bash
curl https://raw.githubusercontent.com/brunoklein99/deep-learning-notes/master/shakespeare.txt -o shakespeare.txt
```

### 4. Check datanode status

```bash
hdfs dfsadmin -report
```

you will see 4 datanode online.

### 5. Wordcount example

```bash
hadoop fs -mkdir /wordcount
```

```bash
hadoop fs -mkdir /wordcount/input
hadoop fs -mkdir /wordcount/output
```

```bash
hadoop fs -put  ./shakespeare.txt /wordcount/input
```

```bash
yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar wordcount /wordcount/input/shakespeare.txt /wordcount/output/test_out
```

```bash
hadoop fs -cat /wordcount/output/test_out/part-r-00000
```

### 6. Pi

```bash
yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar pi 2 10000
```

### 7. Secondary Sort

```bash
hadoop fs -mkdir -p /s_sort/input
hadoop fs -mkdir -p /s_sort/output
```

```bash
vi s_sort.txt
```

```txt
123,555
2781,2144
1,6
7,2
511,47
32,133
90,11
217,12
12,13
```

```bash
hadoop fs -put  ./s_sort.txt /s_sort/input
```

```bash
yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar secondarysort /s_sort/input/s_sort.txt /s_sort/output/ss
```