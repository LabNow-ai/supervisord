# Doc for Debugging

## Debugging the Docker Image

```shell
docker run --rm -it \
  --name app \
  -p 19001:9001 \
  -p 10080:80 \
  -v $(pwd):/data \
  --entrypoint=/bin/bash \
  qpod/supervisord:ubuntu


mkdir -pv /var/log/supervisord
/opt/supervisord/supervisord -c ./supervisord.conf
```

## Replace names and organize imports in code

```bash
function replace_str_in_file() {
  local file_path="$1"
  local name_pattern="$2"
  local str_search="$3"
  local str_replace="$4"
  # Find all .go files in the target directory recursively
  find "${file_path}"     -type f \( -name "${name_pattern}" \) | while read -r FILE; do
      echo "Replace ${str_search} with ${str_replace} in: $FILE" && sed -i "s/${str_search}/${str_replace}/" "$FILE"
  done
}

replace_str_in_file "./"     "*.go"  "github.com\/ochinchina\/supervisord" "supervisord"
```
