# -# 优联悦动 (YouLianYueDong) BLE 设备接入协议

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Protocol Version](https://img.shields.io/badge/Protocol-v1.0.0-green.svg)]()
[![BLE](https://img.shields.io/badge/BLE-GATT_Custom_Service-orange.svg)]()

## 📖 简介
本仓库开源了 **优联悦动 App** 的底层蓝牙通信协议与设备接入规范。我们致力于构建开放的音频设备生态，欢迎第三方硬件厂商、开发者基于本协议将您的音频设备接入优联悦动 App，享受 AI 调音、专业音效与智能控制能力。

> ⚠️ **声明**：本仓库仅公开 BLE 通信接口规范与数据包结构。优联悦动 App 核心代码、AI 算法及 UI 资源均为闭源商业资产，不在本开源范围内。

## ✨ 接入优势
- 🎛️ **统一控制**：音量、输入源、音效模式、EQ 等全量控制接口
- 🤖 **AI 赋能**：支持自然语言 AI 调音指令透传
- 📦 **轻量协议**：固定帧头尾设计，解析简单，兼容性强
- 🌐 **生态共享**：接入设备可共享优联悦动用户流量与会员权益

## 🚀 快速开始

### 1. 蓝牙服务配置
第三方设备需在 BLE GATT 中广播自定义 Service 与 Characteristic：
| 属性 | UUID | 权限 | 说明 |
|------|------|------|------|
| Service | `0000FFF0-0000-1000-8000-00805F9B34FB` | - | 优联悦动控制服务 |
| Characteristic (Write) | `0000FFF1-0000-1000-8000-00805F9B34FB` | Write / WriteWithoutResponse | App → 设备指令下发 |
| Characteristic (Notify) | `0000FFF2-0000-1000-8000-00805F9B34FB` | Notify | 设备 → App 状态上报 |

### 2. 数据包结构
所有通信均遵循统一帧格式：
