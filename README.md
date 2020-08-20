

# 关于C2外包 
1. C2外包使用单独编译的程序，教程按照：
  目前的分支号是cddc56607e1d851e-webapi,详细的教程可以见这个文档 

    [Filecoin Snark计算API接口使用手册.docx](https://kdocs.cn/l/sygDgqBm7?f=111)
2. 系统中将会有两个lotus-storage-miner（C2外包的版本和我们优化的版本，注意C2外包的版本程序一定不能跑P1和P2）


# 关于环境变量


这些环境变量仅对P1/P2起作用，只需要给运行P1/P2 的AMD版本配置。

FIL_PROOFS_ADDPIECE_CACHE: 缓存的空预处理好的add_piece所在的位置，如果为空，表示不跳过add_piece，如果有值，生成或使用该目录下的文件

FIL_PROOFS_USE_SSD_CACHE =1 或其它， 是否使用FIL_PROOFS_SSD_PARENT作为缓存路径，如果使用，cache中的文件临时生成在这个路径上，生成后再转移到实际的目标路径中去

FIL_PROOFS_SSD_PARENT="/opt/local_ssd/SSD_PARENT" 临时的cache文件的缓存路径

**注意** 在做P2时，直接写入分布式存储将会导致P2速度慢，因此还是需要设置FIL_PROOFS_SSD_PARENT，需要将这个值设置成/dev/shm，这样将会在内存中存储P2产生tree-c/tree-r-last文件，生成完毕后自动移动到文件系统上。 

FIL_PROOFS_RESERVED_MEMORY=40 系统保留的内存，是一个数字，以G为单位，为了安全起见一般选为40

XJRW_SHOW_LOGS =y 打开更详细的日志

### 
RUST_LOG="trace" FIL_PROOFS_ADDPIECE_CACHE="/mnt/ssd/bench/piece32G"  FIL_PROOFS_SDR_PARENTS_CACHE_SIZE=65536 FIL_PROOFS_USE_SSD_CACHE=1 FIL_PROOFS_USE_GPU_TREE_BUILDER=1 FIL_PROOFS_USE_GPU_COLUMN_BUILDER=1  XJRW_SHOW_LOG=y XJRW_SHOW_LOGS=y FIL_PROOFS_SSD_PARENT="/mnt/ssd/bench/$2" FIL_PROOFS_PARAMETER_CACHE="/home/zhu/filecoin-proof-parameters-v28" FIL_PROOFS_PARENT_CACHE="/mnt/ssd/parent" ........
