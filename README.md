import os
import random
from moviepy.editor import ImageSequenceClip, AudioFileClip

# 文件夹路径
image_folder = "images"
audio_folder = "audios"
output_path = "output.mp4"

# 参数
image_duration = 2  # 每张图片展示时长，秒

# 获取图片和音频文件列表
images = [os.path.join(image_folder, f) for f in os.listdir(image_folder) if f.lower().endswith(('.jpg', '.png', '.jpeg'))]
audios = [os.path.join(audio_folder, f) for f in os.listdir(audio_folder) if f.lower().endswith(('.mp3', '.wav', '.aac'))]

# 随机排序
random.shuffle(images)
random.shuffle(audios)

# 创建视频片段
clip = ImageSequenceClip(images, durations=[image_duration]*len(images))

# 随机选择一首音频（或拼接多首，请自行修改）
audio_path = random.choice(audios)
audioclip = AudioFileClip(audio_path).subclip(0, clip.duration)
clip = clip.set_audio(audioclip)

# 导出视频
clip.write_videofile(output_path, fps=24)
print("有声相册已生成：", output_path)
