
vim ddr_data_1frame_result_biaomin.bin
:%!xxd

---------------------------------------------------------------------------------
sudo dmesg -c

cat /var/log/kern.log|grep irq

dmesg|grep irq

lspci

cd /home/fpga/qq/Xilinx201704/Vivado/2017.4/bin
sudo sh vivado

cd /home/fpga/qq/minbiao/xdma_driver/driver
sudo insmod xdma.ko

cd /home/fpga/qq/minbiao/xdma_driver/tests_bias_x64
sudo python test_file.py
./dma_from_device -d /dev/xdma0_c2h_0 -a 0x98000000 -s 0x18800 -c 1 -f ./test_rd_ddr


//----waddr*4
./reg_rw /dev/xdma0_user 0xbc w 0x5aa5
./reg_rw /dev/xdma0_user 0xbc w

//----interrupt clear
./reg_rw /dev/xdma0_user 0x28 w 0x1

//----interrupt read
./reg_rw /dev/xdma0_user 0x28 w

./dma_to_device   -d /dev/xdma0_h2c_0 -a 0x90000000 -s 0x52ac0 -c 1 -f ./fpga_data_bin/F_conv1_3x3_padded
./dma_from_device -d /dev/xdma0_c2h_0 -a 0x90000000 -s 0x52ac0 -c 1 -f ./rdata_pic

./dma_to_device   -d /dev/xdma0_h2c_0 -a 0x80000000 -s 0x973000 -c 1 -f ./fpga_data_bin/F_hcnet_64_weight
./dma_from_device -d /dev/xdma0_c2h_0 -a 0x80000000 -s 0x973000 -c 1 -f ./rdata_weight

./dma_to_device   -d /dev/xdma0_h2c_0 -a 0x88000000 -s 0x6c40 -c 1 -f ./fpga_data_bin/F_hcnet_64_bias
./dma_from_device -d /dev/xdma0_c2h_0 -a 0x88000000 -s 0x6c40 -c 1 -f ./rdata_bias

