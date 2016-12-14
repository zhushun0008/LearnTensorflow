```
# Configure enviroments
export PATH=/home/admin/zhushun/software/anaconda2/bin:$PATH
source $HADOOP_HOME/libexec/hadoop-config.sh
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/jre/lib/amd64/server
CLASSPATH=$($HADOOP_HDFS_HOME/bin/hdfs classpath --glob) ipython
#export PATH=/home/admin/zhushun/software/anaconda2/bin:$PATH





# Demo scripts in IPython
import tensorflow as tf
filename_queue = tf.train.string_input_producer(["hdfs://default/user/jd_ad/zhushun/projects/test/aaa.csv","hdfs://default/user/jd_ad/zhushun/projects/test/bbb.csv"])
reader = tf.TextLineReader()
key, value = reader.read(filename_queue) # filename_queue可以有多个文件，key应该是文件号，value是文件内容
record_defaults = [[1], [1]]
col4, col5 = tf.decode_csv(value, record_defaults=record_defaults)
with tf.Session() as sess:
	coord = tf.train.Coordinator()
	threads = tf.train.start_queue_runners(coord=coord)
	for i in range(6):
		print(sess.run([col4, col5])
		
		
# Results
[11, 1]
[12, 1]
[13, 0]
[2, 1]
[3, 1]
[4, 0]
```
