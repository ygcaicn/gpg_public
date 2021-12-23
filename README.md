# gpg_public

```bash
gpg --import pub.asc

gpg --keyserver pgp.mit.edu --search-key 7CF1D03903C103D2
gpg --keyserver keyserver.ubuntu.com --search-key 7CF1D03903C103D2
gpg --keyserver keys.openpgp.org --search-key 7CF1D03903C103D2

gpg --keyserver keys.openpgp.org --recv-keys 7CF1D03903C103D2

gpg --fingerprint

# Verify fingerprint
# 0E0B E3A4 97B0 307A FF7E  CC04 7CF1 D039 03C1 03D2

gpg --recipient 7CF1D03903C103D2 --output demo.tar.gpg --encrypt demo.tar

# Text mode
gpg -a --recipient 7CF1D03903C103D2 --output demo.txt.gpg --encrypt demo.txt

echo Hello | gpg -a -r 7CF1D03903C103D2 -e

# Multiple files
find . -type f -not -name "*.gpg" -print0 | while read -d $'\0' file
do
    if [ -f "$file.gpg" ]; then
        echo "$file.gpg"
        continue
    fi;
    gpg --batch --yes -r 7CF1D03903C103D2 -o "$file.gpg" -e "$file"
    if [ $? -eq 0 ]; then
        echo "$file->$file.gpg remove origin."
        rm -f "$file"
    else
        echo "$file encrypt failed."
    fi
done
```

```bash
gpg --keyserver keys.openpgp.org --recv-keys 10642018D86B4426

# Verify fingerprint
# A51A 946E 217A AB50 F7CB  4255 1064 2018 D86B 4426

gpg -r 10642018D86B4426 -o demo.tar.gpg -e demo.tar
```
