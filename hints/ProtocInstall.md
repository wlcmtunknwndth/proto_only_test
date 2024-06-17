1. Заходим сюда: https://grpc.io/docs/languages/go/quickstart/
2. Устанавливаем protoc: https://github.com/protocolbuffers/protobuf/releases
    2.1. Распаковываем в любую папку. Копируем путь bin папки внутри. 
    2.2. Добавляем переменную окружения. Можно через GUI(ищем system variables), можно через set:
   - set PATH="%PATH%;%(go env GOPATH)%/bin"
   - set PATH="%PATH%;D:\protobuf\protoc-27.1-win64\bin""
3. Запуск программы для генерации кода:
   3.1. protoc -I protos\proto protos\proto\sso\sso.proto --go_out=.\protos\gen\go --go_opt=paths=source_relative --go-grpc_out=.\protos\gen\go\ --go-grpc_opt=paths=source_relative
   1. -I proto — опция -I или —proto_path указывает путь к корневой директории с файлами .proto. Это нужно, чтобы компилятор смог найти импорты, если они есть. В нашем случае это директория proto.
   2. proto/sso/sso.proto — путь к конкретному .proto файлу, который мы компилируем.
   3. —go_out=./gen/go/ — опция —go_out указывает, куда записывать сгенерированный код Go.
   4. —go_opt=paths=source_relative — дополнительная опция, которая указывает, как создавать имена пакетов. paths=source_relative означает, что выходные файлы будут иметь тот же пакет, что и исходные файлы .proto.
   5. —go-grpc_out=./gen/go/ — указывает, куда записывать сгенерированный Go gRPC-код. Как и в предыдущем случае, выходные файлы будут помещены в директорию ./gen/go/.
   6. —go-grpc_opt=paths=source_relative — это аналогичная опция для генерации Go gRPC-кода, которая указывает, как создавать имена пакетов для gRPC.

4. Потом можно go mod tidy, если код уже сгенерирован внутри пакета, а не добавляется извне, чтобы скачать все зависимости
5. Если прото-контракты отдельный пакет, то можем добавить через go get github.com/wlcmtunknwndth/proto
6. Если что-то меняем, то используем git tag v0.0.1 (цифры меняем)

Пример: 
- https://selectel.ru/blog/tutorials/go-grcp/?utm_source=youtube.com&utm_medium=referral&utm_campaign=help_tgbot-grcp_181123_tuzov_paid 
- https://www.youtube.com/watch?v=EURjTg5fw-E&t=889s