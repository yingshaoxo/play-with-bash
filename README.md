# play-with-bash

Let's play bash.

## Environment set up

Jupyter-lab, and:

```bash
pip install bash_kernel
python -m bash_kernel.install
```

## Minimum bash example

```bash
#!/bin/bash

function hi() {
    #no matter what get print out, it will get returned
    author=$1
    echo "${author}: \n"
    echo "hi,\n";
    echo "you";
}

#yingshaoxo="$(echo yingshaoxo)"
yingshaoxo="yingshaoxo"
var=$(hi $yingshaoxo)

echo -e $var
echo -e $var
echo -e "\n"

my_list=("dog" "human" "cat");
for word in ${my_list[@]}; do
    if [[ $word == "human" ]] ; then
        echo "${word} !!!"
    elif [[ $word == "dog" ]]; then
        echo "$word ."
    else
        echo $word
    fi
done

exit
```

## More advanced example

https://leetcode.com/problems/word-frequency

```bash
#!/bin/bash

#2022/12/13 05:32
text=`cat words.txt`
#echo "${text}"

new_text=`echo $text | sed -e 's/\n/ /g'`
#echo "${new_text}"

IFS=' '; splits_list=($new_text); unset IFS

declare -A word_map

function count_by_using_map() {
    # Here $1 is the first parameter, $2 the second, etc.
    word=$1;

    if [[ -v "word_map[$word]" ]] ; then
        word_map[$word]=$((word_map[$word] + 1));
    else
        word_map[$word]=1;
    fi
}

IFS=' '; # Set space as the delimiter
(
    for word in "${splits_list[@]}";
    do
        count_by_using_map $word;
    done

    for word in "${!word_map[@]}"
    do
        echo "${word} ${word_map[$word]}";
    done | sort -n -r -k 2
    # sort -n -k 2
)
unset IF
#2022/12/13 08:14
```

# My thinking

If you could use Python to solve the problem, don't use bash.
