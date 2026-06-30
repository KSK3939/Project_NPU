FPGA parameter export for GAP Dense9 model
=========================================

MODEL_PATH   : ./models/wafer_cnn_conv_keep_gap_dense9_0.922.h5
OUT_DIR      : ./fpga_params_gap_dense9_mem
MEM_DIR      : ./fpga_params_gap_dense9_mem\mem
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
gap_fc_w.mem
gap_fc_b.mem

Expected GAP Dense9 Verilog sizes
---------------------------------
conv1_w  : 3 * 3 * 1  * 8  = 72 entries, int8
conv1_b  : 8 entries, int64 hex
conv2_w  : 3 * 3 * 8  * 16 = 1152 entries, int8
conv2_b  : 16 entries, int64 hex
conv3_w  : 3 * 3 * 16 * 32 = 4608 entries, int8
conv3_b  : 32 entries, int64 hex
gap_out  : 32 entries
gap_fc_w : 32 * 9 = 288 entries, int8
gap_fc_b : 9 entries, int64 hex

GAP formula
-----------
gap_out[c] = sum(pool3[h,w,c] for h=0..5, w=0..5) / 36

FC address formula
------------------
gap_fc_w_addr = channel_index * 9 + class_index

Verilog readmemh example
------------------------
$readmemh("conv1_w.mem",  conv1_w);
$readmemh("conv1_b.mem",  conv1_b);
$readmemh("bn1_mul.mem",  bn1_mul);
$readmemh("bn1_add.mem",  bn1_add);
$readmemh("conv2_w.mem",  conv2_w);
$readmemh("conv2_b.mem",  conv2_b);
$readmemh("bn2_mul.mem",  bn2_mul);
$readmemh("bn2_add.mem",  bn2_add);
$readmemh("conv3_w.mem",  conv3_w);
$readmemh("conv3_b.mem",  conv3_b);
$readmemh("bn3_mul.mem",  bn3_mul);
$readmemh("bn3_add.mem",  bn3_add);
$readmemh("gap_fc_w.mem", gap_fc_w);
$readmemh("gap_fc_b.mem", gap_fc_b);
