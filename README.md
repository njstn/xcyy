100部小马拉大车视频国内真实小马拉大车

using System;
using System.Net.Sockets;
using Modbus.Device;  // 引入 NModbus 库
 
class Program
{
    static void Main(string[] args)
    {
        // 1. 连接到 Modbus 服务器（Modbus TCP）
        string ipAddress = "192.168.0.100"; // 设备的 IP 地址
        int port = 502; // Modbus TCP 默认端口
        var client = new TcpClient(ipAddress, port);
 
        // 2. 获取 Modbus TCP 设备的协议客户端
        var modbusTcpMaster = ModbusTcpMaster.CreateIp(client);
 
        // 3. 读取从站设备的寄存器
        ushort startAddress = 0;  // 寄存器起始地址
        ushort numRegisters = 10; // 读取 10 个寄存器
 
        try
        {
            // 读取保持寄存器
            ushort[] registers = modbusTcpMaster.ReadHoldingRegisters(startAddress, numRegisters);
            
            // 输出结果
            Console.WriteLine("读取到的寄存器值：");
            foreach (var register in registers)
            {
                Console.WriteLine(register);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"读取错误: {ex.Message}");
        }
 
        // 4. 关闭连接
        client.Close();
    }
}
