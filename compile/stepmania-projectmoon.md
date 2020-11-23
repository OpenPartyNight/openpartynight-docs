# StepMania (Project Moon)

The OutFox team is currently developing a closed-source, ground-up rebuild of StepMania. There are plans to open the code in the future, meanwhile, here are notes for using the Alpha builds (available on their website) to get StepMania running on a Pi.

## Log Files & Troubleshooting

Logs are stored under `~/.stepmania-5.3/Logs/`

### Locale Error

```
terminate called after throwing an instance of 'std::runtime_error'
  what():  locale::facet::_S_create_c_locale name not valid
Aborted
```

Fix
```
sudo vim /etc/locale.gen # uncomment en_US UTF-8

sudo locale-gen en_US.UTF-8

sudo update-locale en_US.UTF-8
```

### Alsa Sound Error

Same error as previous StepMania

```
/////////////////////////////////////////
WARNING: ALSA: snd_pcm_wait: Broken pipe
/////////////////////////////////////////
/////////////////////////////////////////
WARNING: ALSA: snd_pcm_wait: Broken pipe
/////////////////////////////////////////
/////////////////////////////////////////
WARNING: ALSA: snd_pcm_wait: Broken pipe
/////////////////////////////////////////
```

Fix
```
# Check output for audio is set to HDMI in raspi-config

# Somehow set SoundDriver=plughw:2,0
```


