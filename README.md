API_ID = "YOUR_API_ID" API_HASH = "YOUR_API_HASH" BOT_TOKEN = "7928071667:AAGoC0-bd6PtHHLPar2ETF6Ona0MK-7kQak"

Initialize bot

bot = Client("Mr_soul", bot_token=BOT_TOKEN, api_id=API_ID, api_hash=API_HASH)

def download_youtube_video(url): ydl_opts = { 'format': 'best', 'outtmpl': 'downloads/%(title)s.%(ext)s' } with yt_dlp.YoutubeDL(ydl_opts) as ydl: info = ydl.extract_info(url, download=True) return ydl.prepare_filename(info)

@bot.on_message(filters.command("start")) def start(client, message): message.reply_text("Welcome! Send me a YouTube or Instagram video URL to download.")

@bot.on_message(filters.text & filters.private) def download_video(client, message): url = message.text if "youtube.com" in url or "youtu.be" in url: message.reply_text("Downloading YouTube video...") file_path = download_youtube_video(url) message.reply_video(file_path) os.remove(file_path) else: message.reply_text("Invalid URL or unsupported website.")

bot.run()
