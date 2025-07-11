import os
import ccxt
import time
from telegram_bot import notify

# قائمة العملات
SYMBOLS = ['PEPE/USDT', 'SHIB/USDT', 'FLOKI/USDT', 'DOGE/USDT', 'WIF/USDT']

# إعدادات الربح والخسارة
TP_PCT = 0.04  # هدف الربح 4%
SL_PCT = 0.02  # وقف خسارة 2%

# الاتصال بـ Binance Testnet
exchange = ccxt.binance({
    'apiKey': os.getenv('BINANCE_API_KEY'),
    'secret': os.getenv('BINANCE_API_SECRET'),
})
exchange.set_sandbox_mode(True)  # تشغيل Sandbox Mode

def main():
    while True:
        for sym in SYMBOLS:
            ticker = exchange.fetch_ticker(sym)
            price = ticker['last']
            notify(f"Watching {sym} at price: {price}")
            # هنا ممكن تضيف مؤشراتك (RSI/EMA) أو شرط بسيط
        time.sleep(15)

if __name__ == "__main__":
    main()
