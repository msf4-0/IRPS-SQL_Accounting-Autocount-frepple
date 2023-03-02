ARG FRAPPE_BRANCH=develop
FROM frappe/erpnext-worker:${FRAPPE_BRANCH}

ARG GITHUB_OWNER=msf4-0 			# you could give a default value as well
ENV GITHUB_OWNER=$GITHUB_OWNER

RUN install_app metabase_integration https://github.com/${GITHUB_OWNER}/ERPNext-Metabase-Integration master && \
  install_app sql_accounting_software https://github.com/${GITHUB_OWNER}/ERPNext-SQL-Accounting-Integration main && \
  install_app erpnext_telegram_integration https://github.com/${GITHUB_OWNER}/ERPNext-Telegram-Integration master && \
  install_app frepple https://github.com/${GITHUB_OWNER}/ERPNext-Frepple-Enhanced-Integration main && \
  install_app barcode_shrdc https://github.com/${GITHUB_OWNER}/ERPNext-Barcode-Integration master && \
  install_app autocount https://github.com/${GITHUB_OWNER}/ERPNext-Autocount-Integration master
