FROM cnadiminti/dynamodb-local:latest

VOLUME ["/dynamodb_local_db"]

EXPOSE 8000

CMD ["--sharedDb", "-dbPath", "/dynamodb_local_db"]