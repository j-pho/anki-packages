# 400kanji-packages

`anki` packages generated via `400kanji-builder`, etc.

for N-kanji packages you have here the output of `step 11` below

for verb conjugations, the process is similar, but see the `conjugation-builder` for the details

## overview of N-kanji process

1. acquire a sorted list of 400 kanji by frequency
2. get 10 sample words for each character
3. produce 3 versions of the word list
- english, kanji+hiragana
- kanji, english+hiragana
- audio, kanji+hiragana+english
4. ask chatgpt for a sample sentence for each word on the word list:
   `i have a list of japanese words. for any given word, please generate a short sample sentence in japanese that uses this word. output the sample sentence in two saparate versions. the first is a kanji version. the second is a hiragana version. next give an english translation of this japanese sentence. repeat this task for each of these words. continue generating sentences until you have performed this task for every item on the list. the list follows. 期待, 招待,...`
5. produce multiple versions of the sentence list
- kanji, english+hiragana
- audio, kanji+hiragana+english
6. use shell scripts to generate the audio files via macOS `say` + `ffmpeg`:
- `shell-scripts/kanji-audio_conversion.sh`
- `shell-scripts/sent-audio_conversion.sh`
7. move audio files into `collection.media`
8. use `400kanji` application to interleave the lists from above:
- `go build`
- `mv 440kanji-builder ./merging`
- `cd ./merging`
- `./400kanji-builder`
9. use `split` to split the merged product into chunks: `shell-scripts/splitter.sh`
10. import each chunk into `anki`
11. export the whole back out from `anki` to an `.apkg`

## caveats

1. irregularities in the `chatgpt` output have not been smoothed over
2. `chatgpt` output; so, buyer beware
3. the number of sentences is out of sync with the number of kanji (*fixme...*)

