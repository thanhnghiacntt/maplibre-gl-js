# Publish lên npm

1. Xem lại [`CHANGELOG.md`](../CHANGELOG.md)
   - Kiểm tra kỹ rằng tất cả các thay đổi nằm trong bản release đã được [ghi lại đúng cách](../CONTRIBUTING.md#changelog-conventions).
   - Các thay đổi sắp được release nên nằm dưới tiêu đề "main".
   - Commit mọi thay đổi cuối cùng vào changelog.
2. Chạy [Create bump version PR](https://github.com/maplibre/maplibre-gl-js/actions/workflows/create-bump-version-pr.yml) bằng cách kích hoạt workflow thủ công (manual workflow dispatch) và nhập số phiên bản vào ô input. Việc này sẽ tạo ra một PR thay đổi changelog và file `package.json` để bạn review và merge.
3. Sau khi merge, một quy trình tự động sẽ được kích hoạt để tạo GitHub release, upload các release asset, và publish kết quả build lên npm.

Workflow này cần secret cấp tổ chức `${{ secrets.NPM_ORG_TOKEN }}` để có thể push lên npm registry.
