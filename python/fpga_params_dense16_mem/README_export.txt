FPGA parameter export for dense16 model
=====================================

MODEL_PATH   : ./models/wafer_cnn_dense16_0.947.h5
OUT_DIR      : ./fpga_params_dense16_mem
MEM_DIR      : ./fpga_params_dense16_mem\mem
INPUT_SCALE  : 128
WEIGHT_SCALE : 64
ACT_SCALE    : 128
BN_SHIFT     : 16

Files for Verilog $readmemh
---------------------------
conv1_w.mem
conv1_b.mem
bn1_mul.mem
bn1_add.mem
conv2_w.mem
conv2_b.mem
bn2_mul.mem
bn2_add.mem
conv3_w.mem
conv3_b.mem
bn3_mul.mem
bn3_add.mem
dense1_w.mem
dense1_b.mem
dense2_w.mem
dense2_b.mem

Expected dense16 Verilog sizes
------------------------------
dense1_w: 1152 * 16 = 18432 entries, int8
dense1_b: 16 entries, int64 hex
dense2_w: 16 * 9 = 144 entries, int8
dense2_b: 9 entries, int64 hex

Dense address formulas
----------------------
dense1: d1w_addr = dense_i * 16 + dense_o
dense2: d2w_addr = dense_i * 9 + dense_o
